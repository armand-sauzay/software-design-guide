## Python Programming Guide

This page aims at defining a set of practices to improve your python code practices. 


### Python Code Principles 
#### Imports
- avoid global imports 

- import modules instead of functions

#### Default values

- no mutable type default value (this will likely cause runtime bugs)

```python
#good 
def append(list, n=None):
    if n: 
    list.append(n)
    return list
```

```python
#bad
def my_function(n, lst=[]):
    lst.append(n)
    return lst

print(my_function(1))  # [1]
print(my_function(2))  # [1, 2]
print(my_function(3))  # [1, 2, 3]
```


Lexical scoping
```python
#bad

# Define a global variable
var = "global"

# Define a function that declares a local variable and a nested function
def my_function():
    var = "local"

    # Define a nested function that declares an enclosing variable
    def my_nested_function():
        var = "enclosing"

        # Print the values of the global, local, and enclosing variables
        print(f"global_var: {global_var}")
        print(f"local_var: {local_var}")
        print(f"enclosing_var: {enclosing_var}")

    # Call the nested function
    my_nested_function()

# Call the function
my_function
```
```python 
#good
# Define a global variable
global_var = "global"

# Define a function that declares a local variable and a nested function
def my_function():
    local_var = "local"

    # Define a nested function that declares an enclosing variable
    def my_nested_function():
        enclosing_var = "enclosing"

        # Print the values of the global, local, and enclosing variables
        print(f"global_var: {global_var}")
        print(f"local_var: {local_var}")
        print(f"enclosing_var: {enclosing_var}")

    # Call the nested function
    my_nested_function()

# Call the function
my_function
```



- limit inheritance
    - use protocols/abstract base classes
    - properties: used to define trivial computation. It should be used so we can’t really see the difference between a property and an attribute but just limit the number of attributes in our class.
```python
#bad
class Circle:
    def __init__(self, radius):
        self.radius = radius

    # Define a property for the circle's area
    @property
    def area(self):
        return 3.14 * self.radius ** 2
```
```python
#good
class Circle:
    def __init__(self, radius):
        self.radius = radius

    # Define a property for the circle's area
    @property
    def area(self):
        return 3.14 * self.radius ** 2
```

- Exception handler
    - you can use them but do not flood code with a lot of try excepts
    - in the example below, if you do not have a try/except logic, your code will crash.

```python
#bad 
# Try to open a file
with open("my_file.txt") as f:
    # Read the file
    data = f.read()

# Handle the case where the file is not found
except FileNotFoundError:
    print("The file was not found.")
```
```python
#good 
try:
    # Try to open a file
    with open("my_file.txt") as f:
        # Read the file
        data = f.read()
except FileNotFoundError:
    # Handle the case where the file is not found
    print("The file was not found.")
except Exception:
    # Handle any other exceptions that may occur
    print("An unexpected error occurred.")
```

- Only one task per function
    - if you have a name with “and” probably, you probably need some refactoring
    - if you have a if/else in the top level of the function, you probably need some refactoring
```python
#bad 
def split_and_rename(df)
  ...
```
```python
#good
def split(df)
  ...
  
def rename(df)
  ...
```

- Use type hints
    - If you don’t have a class readily available, you can use (from typing import Callable)
```python
#bad
def split(df):
  ...
```
```python
#good
def split(df: pd.DataFrame)-> Tuple[pd.DataFrame, pd.DataFrame]:
```

- Separate commands/compute and queries
```python
#bad 
def preprocess(record):
  record.age = data.date - data.birthdate
  return record.age
```
```python 
#good
def preprocess(record)
  return data.date-data.birthdate
#then call this elsewhere
```

- Only include arguments you need

```python
#bad
def split(myClass): 
  data = myClass.data
```
  
```python
#good
def split(data): 
  ...split(data)
```

- Make arguments required
```python
#bad
def func(arg1, arg2 etc): 
  ...

func(a,b,c)
```
```python 
#good
def func(*, arg1,arg2,arg3)
  ...
  #the star forces to have those

func(arg1=a, arg2=b, arg3=c)
```

- Separate object creation and use (dependency injection)
```python 
#bad 
def split(data)
  handler=DataHandler(data)
  handler.handle(data)
```
```python
#good
def split(df: pd.DataFrame, handler: Handler)
  handler.handle(df)
```

- use a main function which contains the main functionality of your code
    - reason: when you import your code you don’t want to accidentally execute code
    - all the code that you put under the if statement below will be available in the global namespace
```
#good
def main():
    ...

if __name__ == '__main__':
    preprocess()
```
```python
#good
def main():
    ...
if __name__ == '__main__':
    main()
```


- Use black in tandem with flake8 and isort to take care of style.