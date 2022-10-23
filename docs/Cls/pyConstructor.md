The **init** method is the constructor. All methods must have self as their first parameter, although it isn't explicitly passed, Python adds the self argument to the list for you; you do not need to include it when you call the methods. Within a method definition, self refers to the instance calling the method.

Classes can have other methods defined to add functionality to them. Remember, that all methods must have self as their first parameter.

Classes can also have class attributes, created by assigning variables within the body of the class. These can be accessed either from instances of the class, or the class itself. Class attributes are shared by all instances of the class.

Trying to access an attribute of an instance that isn't defined causes an AttributeError. This also applies when you call an undefined method.

``` py
class Dog:
  legs=4
  def __init__(self,name, color):
    self.name=name
    self.color=color
  def bark(self):
    print("WooF!")
fido = Dog("Fido","Brown")
print(fido.legs)
fido.bark()
print(Dog.legs)
```
```
4
WooF!
4
```
## Polymorphism

Python does not support explicit multiple constructors, yet there are some ways in which using the multiple constructors can be achieved. If multiple __init__ methods are written for the same class, then the latest one overwrites all the previous constructors.

The class constructors can be made to exhibit polymorphism in three ways which are listed below.

1. [Overloading constructors based on arguments.](#overloading-constructors-based-on-arguments)
2. [Calling methods from __init__.](#calling-methods-from-init)
3. [Using @classmethod decorator.](#using-classmethod-decorator)
4. With python3, you can use Implementing Multiple Dispatch with Function Annotations as [Python Cookbook](https://github.com/dabeaz/python-cookbook/blob/master/src/9/multiple_dispatch_with_function_annotations/example1.py)

### Overloading constructors based on arguments

``` py
class sample:

	# constructor overloading based on args
	def __init__(self, *args):

		# if args are more than 1
		# sum of args
		if len(args) > 1:
			self.ans = 0
			for i in args:
				self.ans += i

		# if arg is an integer
		# square the arg
		elif isinstance(args[0], int):
			self.ans = args[0]*args[0]

		# if arg is string
		# Print with hello
		elif isinstance(args[0], str):
			self.ans = "Hello! "+args[0]+"."


s1 = sample(1, 2, 3, 4, 5)
print("Sum of list :", s1.ans)

s2 = sample(5)
print("Square of int :", s2.ans)

s3 = sample("PolloPitas")
print("String :", s3.ans)

```
```
Sum of list : 15
Square of int : 25
String : Hello! PolloPitas.
```
### Calling methods from __init__

``` py
class eval_equations:

# single constructor to call other methods
	def __init__(self, *inp):

		# when 2 arguments are passed
		if len(inp) == 2:
			self.ans = self.eq2(inp)

		# when 3 arguments are passed
		elif len(inp) == 3:
			self.ans = self.eq1(inp)

		# when more than 3 arguments are passed
		else:
			self.ans = self.eq3(inp)

	def eq1(self, args):
		x = (args[0]*args[0])+(args[1]*args[1])-args[2]
		return x

	def eq2(self, args):
		y = (args[0]*args[0])-(args[1]*args[1])
		return y

	def eq3(self, args):
		temp = 0
		for i in range(0, len(args)):
			temp += args[i]*args[i]
		
		temp = temp/max(args)
		z = temp
		return z


inp1 = eval_equations(1, 2)
inp2 = eval_equations(1, 2, 3)
inp3 = eval_equations(1, 2, 3, 4, 5)

print("equation 2 :", inp1.ans)
print("equation 1 :", inp2.ans)
print("equation 3 :", inp3.ans)

```
```
equation 2 : -3
equation 1 : 2
equation 3 : 11.0
```
### Using @classmethod decorator

``` py
class eval_equations:

	# basic constructor
	def __init__(self, a):
		self.ans = a

	# expression 1
	@classmethod
	def eq1(cls, args):
		
	# create an object for the class to return
		x = cls((args[0]*args[0])+(args[1]*args[1])-args[2])
		return x

	# expression 2
	@classmethod
	def eq2(cls, args):
		y = cls((args[0]*args[0])-(args[1]*args[1]))
		return y

	# expression 3
	@classmethod
	def eq3(cls, args):
		temp = 0

		# square of each element
		for i in range(0, len(args)):
			temp += args[i]*args[i]

		temp = temp/max(args)
		z = cls(temp)
		return z


li = [[1, 2], [1, 2, 3], [1, 2, 3, 4, 5]]
i = 0

# loop to get input three times
while i < 3:

	inp = li[i]

	# no.of.arguments = 2
	if len(inp) == 2:
		p = eval_equations.eq2(inp)
		print("equation 2 :", p.ans)

	# no.of.arguments = 3
	elif len(inp) == 3:
		p = eval_equations.eq1(inp)
		print("equation 1 :", p.ans)

	# More than three arguments
	else:
		p = eval_equations.eq3(inp)
		print("equation 3 :", p.ans)

	#increment loop		
	i += 1

```
```
equation 2 : -3
equation 1 : 2
equation 3 : 11.0
```