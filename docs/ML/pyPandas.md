Pandas is a Python module that helps us read and manipulate data. What's cool about pandas is that you can take in data and view it as a table that's human readable, but it can also be interpreted numerically so that you can do lots of computations with it. Pandas is derived from the term "panel data", an econometrics term for data sets that include observations over multiple time periods for the same individuals.

We call the table of data a DataFrame. A Series is essentially a column, and a DataFrame is a multi-dimensional table made up of a collection of Series. As numpy ndarrays are homogeneous, pandas relaxes this requirement and allows for various dtypes in its data structures.

**Asking for Help**

`help(pd.Series.loc)`

## Series

The Series is one building block in pandas. Pandas Series is a one-dimensional labeled array that can hold data of any type (integer, string, float, python objects, etc.), similar to a column in an excel spreadsheet. The axis labels are collectively called index.

If we are given a bag of letters a, b, and c, and count how many of each we have, we find that there are 1 a, 2 b’s, and 3 c’s. We could create a Series by supplying a list of counts and their corresponding labels.

If we don’t specify the index, by default, the index would be the integer positions starting from 0.

Accessing the value by its index, rather than the integer position comes in handy when the dataset is of thousands, if not millions, of rows. Series is the building block for the DataFrame we will introduce next.

Think of Series as numpy 1d array with index or row names.

``` py
import pandas as pd
import numpy as np
s1=pd.Series([1,2,3],index=['a','b','c'])
#Alternatively, the values can be a numpy array:
s2=pd.Series(np.array([1,2,3]),index=['a','b','c'])
#Or, we could use a dictionary to specify the index with keys
s3=pd.Series({'a':1,'b':2,'c':3})
#In a Series, we can access the value by its index directly
s3['a']
```
```
1
```

## DataFrames

In data science, data is usually more than one-dimensional, and of different data types; thus Series is not sufficient. DataFrames are 2darrays with both row and column labels. The easiest way to create a DataFrame is using a dictionary. Each key is a column, while the value is an array representing the data for that column.And then, we can pass this dictionary to the DataFrame constructor.

The DataFrame automatically creates a numeric index for each row. We can specify a custom index, when creating the DataFrame. We can access a row using its index and the loc[] function. loc uses square brackets to specify the index.

``` py
import pandas as pd

data = {
   'ages': [14, 18, 24, 42],
   'heights': [165, 180, 176, 184]
} 
df=pd.DataFrame(data)


df=pd.DataFrame(data, index=['James', 'Bob','Ana','Susan'])
print(df.loc["Bob"])
```
```
ages        18
heights    180
Name: Bob, dtype: int64
```

Similar to numpy, to get the dimensions of a DataFrame, use .shape

Size also works on DataFrame to return an integer representing the number of elements in this object.

## Importing and Exporting Data

Generally data is stored in CSV (comma-separated values) files, which we can easily read in with panda’s read_csv function. Pandas also supports reading from JSON files, as well as SQL databases.

* The **head** method returns the first 5 rows. You can instruct it to return the number of rows you would like as an argument (for example, df.head(10) will return the first 10 rows). Similarly, you can get the last rows using the **tail()** function.

* The **info()** function is used to get essential information about your dataset, such as number of rows, columns, data types, etc. Pandas automatically generates an index for the DataFrame, if none is specified. We can set our own index column by using the set_index() function.
`df.setIndex("Sex", inplace=True)`
The inplace=True argument specifies that the change will be applied to our DataFrame, without the need to assign it to a new DataFrame variable.

* The **describe** method returns a table of statistics about the columns. We add a line in the code below to force python to display all 6 columns. Without the line, it will abbreviate the results. We can also get the summary stats for a single column.

    - Count: This is the number of rows that have a value. In our case, every passenger has a value for each of the columns, so the value is 887 (the total number of passengers).
    - Mean: Recall that the mean is the standard average.
    - Std: This is short for standard deviation. This is a measure of how dispersed the data is.
    - Min: The smallest value
    - 25%: The 25th percentile
    - 50%: The 50th percentile, also known as the median.
    - 75%: The 75th percentile
    - Max: The largest value

  **.describe()** ignores the null values, such as `NaN` (Not a Number) and generates the descriptive statistics that summarize the central tendency (i.e., mean), dispersion (i.e., standard deviation), and shape (i.e., min, max, and quantiles) of a dataset’s distribution.

  **df.shape**

  **df.index** : Describe index

  **df.columns**

  **df.count()** : Number of non-NA values

### CSV

``` py
import pandas as pd 
#read csv
df = pd.read_csv('titanic.csv')
#write csv
df.to_csv('titanic.csv')
print(df.head())
pd.options.display.max_columns=6
```
```
   Unnamed: 0  Survived  Pclass  ... Siblings/Spouses  Parents/Children  \
0           0         0       3  ...                1                 0   
1           1         1       1  ...                1                 0   
2           2         1       3  ...                0                 0   
3           3         1       1  ...                1                 0   
4           4         0       3  ...                0                 0   

      Fare  
0   7.2500  
1  71.2833  
2   7.9250  
3  53.1000  
4   8.0500  

[5 rows x 8 columns]
```

``` py
df.info()
```
```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 887 entries, 0 to 886
Data columns (total 7 columns):
 #   Column            Non-Null Count  Dtype  
---  ------            --------------  -----  
 0   Survived          887 non-null    int64  
 1   Pclass            887 non-null    int64  
 2   Sex               887 non-null    object 
 3   Age               887 non-null    float64
 4   Siblings/Spouses  887 non-null    int64  
 5   Parents/Children  887 non-null    int64  
 6   Fare              887 non-null    float64
dtypes: float64(2), int64(4), object(1)
memory usage: 48.6+ KB
```

``` py
print(df.describe())
```
```
*****Describe****
         Survived      Pclass         Age  Siblings/Spouses  Parents/Children  \
count  887.000000  887.000000  887.000000        887.000000        887.000000   
mean     0.385569    2.305524   29.471443          0.525366          0.383315   
std      0.487004    0.836662   14.121908          1.104669          0.807466   
min      0.000000    1.000000    0.420000          0.000000          0.000000   
25%      0.000000    2.000000   20.250000          0.000000          0.000000   
50%      0.000000    3.000000   28.000000          0.000000          0.000000   
75%      1.000000    3.000000   38.000000          1.000000          0.000000   
max      1.000000    3.000000   80.000000          8.000000          6.000000   

            Fare  
count  887.00000  
mean    32.30542  
std     49.78204  
min      0.00000  
25%      7.92500  
50%     14.45420  
75%     31.13750  
max    512.32920  
```

``` py
print(df['Survived'].describe())
```
```
count    887.000000
mean       0.385569
std        0.487004
min        0.000000
25%        0.000000
50%        0.000000
75%        1.000000
max        1.000000
Name: Survived, dtype: float64
```
### Excel

``` py
#Read
xlsx = pd.ExcelFile('file.xls')
df = pd.read_excel(xlsx,  'Sheet1')
#Write
df.to_excel('dir/myDataFrame.xlsx',  sheet_name='Sheet1')
```

### SQL

(read_sql()is a convenience wrapper around read_sql_table() and read_sql_query())


``` py
from sqlalchemy import create_engine
engine = create_engine('sqlite:///:memory:')
pd.read_sql(SELECT * FROM my_table;, engine)
pd.read_sql_table('my_table', engine)
pd.read_sql_query(SELECT * FROM my_table;', engine)
df.to_sql('myDf', engine)
```

## Selecting Columns

We often will only want to deal with some of the columns that we have in our dataset. To select a single column, we use the square brackets and the column name. The result is what we call a Pandas Series. A series is like a DataFrame, but it's just a single column.

**Selecting Multiple Columns**

We can also select multiple columns from our original DataFrame, creating a smaller DataFrame. We're going to select just the Age, Sex, and Survived columns from our original DataFrame.

When selecting a single column from a Pandas DataFrame, we use single square brackets. When selecting multiple columns, we use double square brackets.

``` py
col = df['Fare']
print(col)
```
```
0       7.2500
1      71.2833
2       7.9250
3      53.1000
4       8.0500
        ...   
882    13.0000
883    30.0000
884    23.4500
885    30.0000
886     7.7500
Name: Fare, Length: 887, dtype: float64
```

``` py
small_df = df[['Age', 'Sex', 'Survived']]
print(small_df.head())
```
```
    Age     Sex  Survived
0  22.0    male         0
1  38.0  female         1
2  26.0  female         1
3  35.0  female         1
4  35.0    male         0
```

## Creating a Column

We can easily create a new column in our DataFrame that is True if the passenger is male and False if they’re female. To create a new column, we use the same bracket syntax (df['male']) and then assign this new value to it.

``` py
df['male'] = df['Sex'] == 'male'
print(df.head())
```
```
   Survived  Pclass     Sex  ...  Parents/Children     Fare   male
0         0       3    male  ...                 0   7.2500   True
1         1       1  female  ...                 0  71.2833  False
2         1       3  female  ...                 0   7.9250  False
3         1       1  female  ...                 0  53.1000  False
4         0       3    male  ...                 0   8.0500   True

[5 rows x 8 columns]
```

## Slicing

Pandas uses the iloc function to select data based on its numeric index. It works the same way indexing lists does in Python. iloc follows the same rules as slicing does with Python lists.

We can also select the data based on a condition.

.loc[ ] allows us to select data by label or by a conditional statement. .loc allows us to access any of the columns.

Both .loc[ ] and .iloc[ ] may be used with a boolean array to subset the data.

``` py
#Third row
print(df.iloc[2])
#First three rows
print(df.iloc[:3])
#rows 2 to 3
print(df.iloc[1:3])

#Conditionals
print(df[df['ages']>18])
#Conditionals
print(df[(df['ages']>18) & ( df['heights']< 180 )])
```
```
ages        24
heights    176
Name: Ana, dtype: int64
       ages  heights
James    14      165
Bob      18      180
Ana      24      176
     ages  heights
Bob    18      180
Ana    24      176
       ages  heights
Ana      24      176
Susan    42      184
     ages  heights
Ana    24      176
```

## Droping a Column

drop() deletes rows and columns. axis=1 specifies that we want to drop a column. axis=0 will drop a row.

``` py
df.drop('Sex',axis=1,inplace=True)
```

## Other Functions

### Value_counts

value_counts() returns how many times a value appears in the dataset, also called the frequency of the values.

``` py
df['Survived'].value_counts()
```
```
0    545
1    342
Name: Survived, dtype: int64
```
### Groupby

The groupby() function is used to group our dataset by the given column. Similarly, we can use min(), max(), mean(), etc. to find the corresponding values for each group.

``` py
df.groupby('Survived')['Age'].value_counts()
```
```
Survived  Age 
0         21.0    28
          28.0    27
          22.0    24
          18.0    23
          30.0    23
                  ..
1         32.5     1
          43.0     1
          53.0     1
          55.0     1
          80.0     1
Name: Age, Length: 146, dtype: int64
```

### Aggregation

We can also perform multiple operations on the groupby object using .agg() method. It takes a string, a function, or a list thereof.

Using groupby and agg provides us the flexibility and therefore the power to look into various perspectives of a variable or column conditioned on categories.

``` py
df.groupby('Survived').agg({'Age':[np.median,np.mean],'Fare':[min,max]})
```
```
            Age	                Fare
            median	mean	    min	max
Survived				
0	        28.0	30.138532	0.0	263.0000
1	        28.0	28.408392	0.0	512.3292
```

### Sort and Rank
``` py
#Sort by labels along an axis
df.sort_index()
```
``` py
#Sort by the values along an axis
df.sort_values(by='Fare') 
```
``` py
#Assign ranks to entries
df.rank()
```

## Dealing with Missing Values

Three approaches to dealing with missing values.

**1) A Simple Option: Drop Columns with Missing Values**

The simplest option is to drop columns with missing values. Unless most values in the dropped columns are missing, the model loses access to a lot of (potentially useful!) information with this approach.

**2) A Better Option: Imputation**

Imputation fills in the missing values with some number. For instance, we can fill in the mean value along each column. The imputed value won't be exactly right in most cases, but it usually leads to more accurate models than you would get from dropping the column entirely.

**3) An Extension To Imputation**

Imputation is the standard approach, and it usually works well. However, imputed values may be systematically above or below their actual values (which weren't collected in the dataset). Or rows with missing values may be unique in some other way. In that case, your model would make better predictions by considering which values were originally missing. In this approach, we impute the missing values, as before. And, additionally, for each column with missing entries in the original dataset, we add a new column that shows the location of the imputed entries.

In some cases, this will meaningfully improve results. In other cases, it doesn't help at all.


``` py
import pandas as pd
from sklearn.model_selection import train_test_split

# Load the data
data = pd.read_csv('https://raw.githubusercontent.com/esabunor/MLWorkspace/master/melb_data.csv')
#print(data.head())
# Select target
y = data.Price

# To keep things simple, we'll use only numerical predictors
melb_predictors = data.drop(['Price'], axis=1)
X = melb_predictors.select_dtypes(exclude=['object'])

# Divide data into training and validation subsets
X_train, X_valid, y_train, y_valid = train_test_split(X, y, train_size=0.8, test_size=0.2,
                                                      random_state=0)
```
**Defining Scoring**

``` py
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_absolute_error

# Function for comparing different approaches
def score_dataset(X_train, X_valid, y_train, y_valid):
    model = RandomForestRegressor(n_estimators=10, random_state=0)
    model.fit(X_train, y_train)
    preds = model.predict(X_valid)
    return mean_absolute_error(y_valid, preds)
```
**Drop columns with missing values**

``` py
# Get names of columns with missing values
cols_with_missing = [col for col in X_train.columns
                     if X_train[col].isnull().any()]

# Drop columns in training and validation data
reduced_X_train = X_train.drop(cols_with_missing, axis=1)
reduced_X_valid = X_valid.drop(cols_with_missing, axis=1)

print("MAE from Approach 1 (Drop columns with missing values):")
print(score_dataset(reduced_X_train, reduced_X_valid, y_train, y_valid))
```
```
MAE from Approach 1 (Drop columns with missing values):
354257.66157608695
```
**Imputation**

Next, we use SimpleImputer to replace missing values with the mean value along each column.

Although it's simple, filling in the mean value generally performs quite well (but this varies by dataset). While statisticians have experimented with more complex ways to determine imputed values (such as regression imputation, for instance), the complex strategies typically give no additional benefit once you plug the results into sophisticated machine learning models.

``` py
from sklearn.impute import SimpleImputer

# Imputation
my_imputer = SimpleImputer()
imputed_X_train = pd.DataFrame(my_imputer.fit_transform(X_train))
imputed_X_valid = pd.DataFrame(my_imputer.transform(X_valid))

# Imputation removed column names; put them back
imputed_X_train.columns = X_train.columns
imputed_X_valid.columns = X_valid.columns

print("MAE from Approach 2 (Imputation):")
print(score_dataset(imputed_X_train, imputed_X_valid, y_train, y_valid))
```
```
MAE from Approach 2 (Imputation):
203078.71828804348
```

**An Extension to Imputation**

Next, we impute the missing values, while also keeping track of which values were imputed.

``` py
# Make copy to avoid changing original data (when imputing)
X_train_plus = X_train.copy()
X_valid_plus = X_valid.copy()

# Make new columns indicating what will be imputed
for col in cols_with_missing:
    X_train_plus[col + '_was_missing'] = X_train_plus[col].isnull()
    X_valid_plus[col + '_was_missing'] = X_valid_plus[col].isnull()

# Imputation
my_imputer = SimpleImputer()
imputed_X_train_plus = pd.DataFrame(my_imputer.fit_transform(X_train_plus))
imputed_X_valid_plus = pd.DataFrame(my_imputer.transform(X_valid_plus))

# Imputation removed column names; put them back
imputed_X_train_plus.columns = X_train_plus.columns
imputed_X_valid_plus.columns = X_valid_plus.columns

print("MAE from Approach 3 (An Extension to Imputation):")
print(score_dataset(imputed_X_train_plus, imputed_X_valid_plus, y_train, y_valid))
```
```
MAE from Approach 3 (An Extension to Imputation):
202839.1169021739
```

Best result is Approach 3, lowest MAE.

## Categorical Variables

A categorical variable takes only a limited number of values.

Consider a survey that asks how often you eat breakfast and provides four options: "Never", "Rarely", "Most days", or "Every day". In this case, the data is categorical, because responses fall into a fixed set of categories. If people responded to a survey about which what brand of car they owned, the responses would fall into categories like "Honda", "Toyota", and "Ford". In this case, the data is also categorical. You will get an error if you try to plug these variables into most machine learning models in Python without preprocessing them first.

**1) Drop Categorical Variables**

The easiest approach to dealing with categorical variables is to simply remove them from the dataset. This approach will only work well if the columns did not contain useful information.

**2) Ordinal Encoding**

Ordinal encoding assigns each unique value to a different integer. This approach assumes an ordering of the categories: "Never" (0) < "Rarely" (1) < "Most days" (2) < "Every day" (3).

This assumption makes sense in this example, because there is an indisputable ranking to the categories. Not all categorical variables have a clear ordering in the values, but we refer to those that do as ordinal variables. For tree-based models (like decision trees and random forests), you can expect ordinal encoding to work well with ordinal variables.

**3) One-Hot Encoding**

One-hot encoding creates new columns indicating the presence (or absence) of each possible value in the original data. To understand this, we'll work through an example.
In contrast to ordinal encoding, one-hot encoding does not assume an ordering of the categories. Thus, you can expect this approach to work particularly well if there is no clear ordering in the categorical data (e.g., "Red" is neither more nor less than "Yellow"). We refer to categorical variables without an intrinsic ranking as nominal variables.

One-hot encoding generally does not perform well if the categorical variable takes on a large number of values (i.e., you generally won't use it for variables taking more than 15 different values).

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

# Drop columns with missing values (simplest approach)
cols_with_missing = [col for col in X_train_full.columns if X_train_full[col].isnull().any()] 
X_train_full.drop(cols_with_missing, axis=1, inplace=True)
X_valid_full.drop(cols_with_missing, axis=1, inplace=True)

# "Cardinality" means the number of unique values in a column
# Select categorical columns with relatively low cardinality (convenient but arbitrary)
low_cardinality_cols = [cname for cname in X_train_full.columns if X_train_full[cname].nunique() < 10 and 
                        X_train_full[cname].dtype == "object"]

# Select numerical columns
numerical_cols = [cname for cname in X_train_full.columns if X_train_full[cname].dtype in ['int64', 'float64']]

# Keep selected columns only
my_cols = low_cardinality_cols + numerical_cols
X_train = X_train_full[my_cols].copy()
X_valid = X_valid_full[my_cols].copy()
```

``` py
X_train.head()
```
```
	        Type	Method	Unnamed: 0	Rooms
    2573	h	    SP	        3349	4
    2091	h	    SP	        2686	3
    4683	u	    S	        6065	2
    8832	h	    VB	        11346	3
    10469	u	    S	        13474	2
```

Next, we obtain a list of all of the categorical variables in the training data.

We do this by checking the data type (or dtype) of each column. The object dtype indicates a column has text (there are other things it could theoretically be, but that's unimportant for our purposes). For this dataset, the columns with text indicate categorical variables.

``` py
# Get list of categorical variables
s = (X_train.dtypes == 'object')
object_cols = list(s[s].index)

print("Categorical variables:")
print(object_cols)
```
```
Categorical variables:
['Type', 'Method']
```
**Define Function to Measure Quality of Each Approach**

We define a function score_dataset() to compare the three different approaches to dealing with categorical variables. This function reports the mean absolute error (MAE) from a random forest model. In general, we want the MAE to be as low as possible!

``` py
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_absolute_error

# Function for comparing different approaches
def score_dataset(X_train, X_valid, y_train, y_valid):
    model = RandomForestRegressor(n_estimators=100, random_state=0)
    model.fit(X_train, y_train)
    preds = model.predict(X_valid)
    return mean_absolute_error(y_valid, preds)
```
**Score from Approach 1 (Drop Categorical Variables)**

We drop the object columns with the select_dtypes() method.

``` py
drop_X_train = X_train.select_dtypes(exclude=['object'])
drop_X_valid = X_valid.select_dtypes(exclude=['object'])

print("MAE from Approach 1 (Drop categorical variables):")
print(score_dataset(drop_X_train, drop_X_valid, y_train, y_valid))
```
```
MAE from Approach 1 (Drop categorical variables):
345278.21768750006
```

**Score from Approach 2 (Ordinal Encoding)**

Scikit-learn has a OrdinalEncoder class that can be used to get ordinal encodings. We loop over the categorical variables and apply the ordinal encoder separately to each column. In the code cell below, for each column, we randomly assign each unique value to a different integer. This is a common approach that is simpler than providing custom labels; however, we can expect an additional boost in performance if we provide better-informed labels for all ordinal variables.

``` py
from sklearn.preprocessing import OrdinalEncoder

# Make copy to avoid changing original data 
label_X_train = X_train.copy()
label_X_valid = X_valid.copy()

# Apply ordinal encoder to each column with categorical data
ordinal_encoder = OrdinalEncoder()
label_X_train[object_cols] = ordinal_encoder.fit_transform(X_train[object_cols])
label_X_valid[object_cols] = ordinal_encoder.transform(X_valid[object_cols])

print("MAE from Approach 2 (Ordinal Encoding):") 
print(score_dataset(label_X_train, label_X_valid, y_train, y_valid))
```
```
MAE from Approach 2 (Ordinal Encoding):
314139.64080978255
```

Fitting an ordinal encoder to a column in the training data creates a corresponding integer-valued label for each unique value that appears in the training data. In the case that the validation data contains values that don't also appear in the training data, the encoder will throw an error, because these values won't have an integer assigned to them.

This is a common problem that you'll encounter with real-world data, and there are many approaches to fixing this issue. For instance, you can write a custom ordinal encoder to deal with new categories. The simplest approach, however, is to drop the problematic categorical columns.

The code cell below save the problematic columns to a Python list bad_label_cols. Likewise, columns that can be safely ordinal encoded are stored in good_label_cols.

``` py
# Categorical columns in the training data
object_cols = [col for col in X_train.columns if X_train[col].dtype == "object"]

# Columns that can be safely ordinal encoded
good_label_cols = [col for col in object_cols if 
                   set(X_valid[col]).issubset(set(X_train[col]))]
        
# Problematic columns that will be dropped from the dataset
bad_label_cols = list(set(object_cols)-set(good_label_cols))
        
print('Categorical columns that will be ordinal encoded:', good_label_cols)
print('\nCategorical columns that will be dropped from the dataset:', bad_label_cols)
```
**Score from Approach 3 (One-Hot Encoding)**

We use the OneHotEncoder class from scikit-learn to get one-hot encodings. There are a number of parameters that can be used to customize its behavior.

We set handle_unknown='ignore' to avoid errors when the validation data contains classes that aren't represented in the training data, and
setting sparse=False ensures that the encoded columns are returned as a numpy array (instead of a sparse matrix).
To use the encoder, we supply only the categorical columns that we want to be one-hot encoded. For instance, to encode the training data, we supply X_train[object_cols]. (object_cols in the code cell below is a list of the column names with categorical data, and so X_train[object_cols] contains all of the categorical data in the training set.)

``` py
from sklearn.preprocessing import OneHotEncoder

# Apply one-hot encoder to each column with categorical data
OH_encoder = OneHotEncoder(handle_unknown='ignore', sparse=False)
OH_cols_train = pd.DataFrame(OH_encoder.fit_transform(X_train[object_cols]))
OH_cols_valid = pd.DataFrame(OH_encoder.transform(X_valid[object_cols]))

# One-hot encoding removed index; put it back
OH_cols_train.index = X_train.index
OH_cols_valid.index = X_valid.index

# Remove categorical columns (will replace with one-hot encoding)
num_X_train = X_train.drop(object_cols, axis=1)
num_X_valid = X_valid.drop(object_cols, axis=1)

# Add one-hot encoded columns to numerical features
OH_X_train = pd.concat([num_X_train, OH_cols_train], axis=1)
OH_X_valid = pd.concat([num_X_valid, OH_cols_valid], axis=1)

print("MAE from Approach 3 (One-Hot Encoding):") 
print(score_dataset(OH_X_train, OH_X_valid, y_train, y_valid))
```
```
MAE from Approach 3 (One-Hot Encoding):
314342.2874402174
```
We refer to the number of unique entries of a categorical variable as the cardinality of that categorical variable.

For large datasets with many rows, one-hot encoding can greatly expand the size of the dataset. For this reason, we typically will only one-hot encode columns with relatively low cardinality. Then, high cardinality columns can either be dropped from the dataset, or we can use ordinal encoding.

``` py
# Get number of unique entries in each column with categorical data
object_nunique = list(map(lambda col: X_train[col].nunique(), object_cols))
d = dict(zip(object_cols, object_nunique))

# Print number of unique entries by column, in ascending order
sorted(d.items(), key=lambda x: x[1])
```
to set low_cardinality_cols to a Python list containing the columns that will be one-hot encoded. Likewise, high_cardinality_cols contains a list of categorical columns that will be dropped from the dataset.

``` py
# Columns that will be one-hot encoded
low_cardinality_cols = [col for col in object_cols if X_train[col].nunique() < 10]

# Columns that will be dropped from the dataset
high_cardinality_cols = list(set(object_cols)-set(low_cardinality_cols))

print('Categorical columns that will be one-hot encoded:', low_cardinality_cols)
print('\nCategorical columns that will be dropped from the dataset:', high_cardinality_cols)
```

**Which approach is best?**

In this case, dropping the categorical columns (Approach 1) performed worst, since it had the highest MAE score. As for the other two approaches, since the returned MAE scores are so close in value, there doesn't appear to be any meaningful benefit to one over the other.

In general, one-hot encoding (Approach 3) will typically perform best, and dropping the categorical columns (Approach 1) typically performs worst, but it varies on a case-by-case basis.