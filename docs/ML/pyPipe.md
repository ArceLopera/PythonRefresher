Pipelines are a simple way to keep your data preprocessing and modeling code organized. Specifically, a pipeline bundles preprocessing and modeling steps so you can use the whole bundle as if it were a single step.

Many data scientists hack together models without pipelines, but pipelines have some important benefits. Those include:

1. **Cleaner Code:** Accounting for data at each step of preprocessing can get messy. With a pipeline, you won't need to manually keep track of your training and validation data at each step.
2. **Fewer Bugs:** There are fewer opportunities to misapply a step or forget a preprocessing step.
3. **Easier to Productionize:** It can be surprisingly hard to transition a model from a prototype to something deployable at scale. .
4. **More Options for Model Validation:** cross-validation.

``` py
import pandas as pd
from sklearn.model_selection import train_test_split

# Read the data
data = pd.read_csv('https://raw.githubusercontent.com/esabunor/MLWorkspace/master/melb_data.csv')

# Separate target from predictors
y = data.Price
X = data.drop(['Price'], axis=1)

# Divide data into training and validation subsets
X_train_full, X_valid_full, y_train, y_valid = train_test_split(X, y, train_size=0.8, test_size=0.2,
                                                                random_state=0)

# "Cardinality" means the number of unique values in a column
# Select categorical columns with relatively low cardinality (convenient but arbitrary)
categorical_cols = [cname for cname in X_train_full.columns if X_train_full[cname].nunique() < 10 and 
                        X_train_full[cname].dtype == "object"]

# Select numerical columns
numerical_cols = [cname for cname in X_train_full.columns if X_train_full[cname].dtype in ['int64', 'float64']]

# Keep selected columns only
my_cols = categorical_cols + numerical_cols
X_train = X_train_full[my_cols].copy()
X_valid = X_valid_full[my_cols].copy()

X_train.head()

```


||Type|	Method|	Regionname|	Unnamed: 0|	Rooms|	Distance|	Postcode|	Bedroom2|	Bathroom|	Car|	Landsize|	BuildingArea|	YearBuilt|	Lattitude|	Longtitude|	Propertycount|
||||||||||||||||||
|2573|	h|	SP|	Northern Metropolitan|	3349|	4|	7.8|	3058.0|	4.0|	2.0|	1.0|	381.0|	NaN|	1938.0|	-37.7337|	144.9548|	11204.0|
|2091|	h|	SP|	Southern Metropolitan|	2686|	3|	7.8|	3124.0|	3.0|	1.0|	1.0|	544.0|	160.0|	1930.0|	-37.8436|	145.0581|	8920.0|
|4683|	u|	S|	Southern Metropolitan|	6065|	2|	5.6|	3101.0|	2.0|	1.0|	1.0|	121.0|	NaN|	NaN|	-37.8126|	145.0534|	10331.0|
|8832|	h|	VB|	Southern Metropolitan|	11346|	3|	7.5|	3123.0|	3.0|	2.0|	2.0|	200.0|	NaN|	NaN|	-37.8396|	145.0514|	6482.0|
|10469|	u|	S|	Southern Metropolitan|	13474|	2|	4.5|	3181.0|	2.0|	1.0|	1.0|	2842.0|	84.0|	1920.0|	-37.8513|	144.9943|	7717.0|

We construct the full pipeline in three steps.

## Step 1: Define Preprocessing Steps

Similar to how a pipeline bundles together preprocessing and modeling steps, we use the ColumnTransformer class to bundle together different preprocessing steps. The code below:

imputes missing values in numerical data, and imputes missing values and applies a one-hot encoding to categorical data. 

``` py
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import OneHotEncoder

# Preprocessing for numerical data
numerical_transformer = SimpleImputer(strategy='constant')

# Preprocessing for categorical data
categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='most_frequent')),
    ('onehot', OneHotEncoder(handle_unknown='ignore'))
])

# Bundle preprocessing for numerical and categorical data
preprocessor = ColumnTransformer(
    transformers=[
        ('num', numerical_transformer, numerical_cols),
        ('cat', categorical_transformer, categorical_cols)
    ])
```


## Step 2: Define the Model
Next, we define a random forest model with the familiar RandomForestRegressor class.


``` py
from sklearn.ensemble import RandomForestRegressor

model = RandomForestRegressor(n_estimators=100, random_state=0)
```

## Step 3: Create and Evaluate the Pipeline
Finally, we use the Pipeline class to define a pipeline that bundles the preprocessing and modeling steps. There are a few important things to notice:

With the pipeline, we preprocess the training data and fit the model in a single line of code. (In contrast, without a pipeline, we have to do imputation, one-hot encoding, and model training in separate steps. This becomes especially messy if we have to deal with both numerical and categorical variables!) With the pipeline, we supply the unprocessed features in X_valid to the predict() command, and the pipeline automatically preprocesses the features before generating predictions. (However, without a pipeline, we have to remember to preprocess the validation data before making predictions.)

``` py
from sklearn.metrics import mean_absolute_error

# Bundle preprocessing and modeling code in a pipeline
my_pipeline = Pipeline(steps=[('preprocessor', preprocessor),
                              ('model', model)
                             ])

# Preprocessing of training data, fit model 
my_pipeline.fit(X_train, y_train)

# Preprocessing of validation data, get predictions
preds = my_pipeline.predict(X_valid)

# Evaluate the model
score = mean_absolute_error(y_valid, preds)
print('MAE:', score)
```
```
MAE: 177453.58753804347
```
Now, you'll use your trained model to generate predictions with the test data.

``` py
# Preprocessing of test data, fit model
preds_test = my_pipeline.predict(X_test)
```
``` py
# Save test predictions to file
output = pd.DataFrame({'Id': X_test.index,
                       'SalePrice': preds_test})
output.to_csv('submission.csv', index=False)
```