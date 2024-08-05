**Benefits of Python:**

* Object-Oriented Language
* High-Level Language
* Dynamically Typed language
* Extensive support Libraries
* Presence of third-party modules
* Open source and community development
* Portable and Interactive
* Portable across Operating systems

**Is Python a compiled language or an interpreted language?**

python is actually partially compiled and partially interpreted language. Because first it compile it and generates byte code using Python virtual machine.

**What is the difference between a Mutable data type and an Immutable data type?**

Mutable Type -> change it's type in run time ex: list, set, dict

Immutable Type -> not change in run time ex: string, tuple

**What is the difference between a set and dictionary?**

| **Parameter**      | **Set**                               | **Dictionary**                                  |
| ------------------------ | ------------------------------------------- | ----------------------------------------------------- |
| **Definition**     | An unordered collection of unique elements. | An ordered collection of key-value pairs.             |
| **Representation** | Curly braces {}.                            | Curly braces {}, but with key-value pairs.            |
| **Order**          | Unordered.                                  | Ordered (from Python 3.7 onwards).                    |
| **Duplicates**     | Does not allow duplicate elements.          | Does not allow duplicate keys.                        |
| **Mutability**     | Mutable (can add or remove elements).       | Mutable (can add, modify, or remove key-value pairs). |
| **Access Method**  | Elements are accessed directly.             | Values are accessed using keys.                       |
| **Use Case**       | To store unique elements.                   | To store related pieces of information.               |
| **Example**        | my_set = {1, 2, 3}                          | my_dict = {“name”: “Alice”, “age”: 30}          |

****Differentiate between List and Tuple?****

| ****List****                                                      | ****Tuple****                                   |
| ----------------------------------------------------------------------------- | ----------------------------------------------------------- |
| Lists are Mutable datatype                                                    | Tuples are Immutable datatype.                              |
| Lists consume more memory                                                     | Tuple consumes less memory as compared to the list          |
| The list is better for performing operations, such as insertion and deletion. | A Tuple data type is appropriate for accessing the elements |
| The implication of iterations is Time-consuming                               | The implication of iterations is comparatively Faster       |

**What is Lambda Function?**

Lambda function is an anonymous function with any numbers of parameters but only with one statement. Anonymous function means function without name and can be immediately stored in a variable.

**What is Pass in Python?**

We use pass statement as a placeholder used for future code and when in else condition we don't want to do anything, because when pass statement execute nothing happens, used for avoid errors and for the scenarios where empty code not allow.

**How is Exceptional Handling done in python?**

We use three keywords i.e try, except and finally

try -> block code allow to test for errors

except -> block code used for error handling

else -> block code used for when not error found

finally -> block code used for execute code without checking try and except block

****Difference between for loop and while loop in Python****

For loop used to iterate through the element lik list,tuple,set,dict, use for loop when there have both start and end condition. Where as while loop have the end condition.

**Can we Pass a function as an argument?**

Yes, we can pass a function as an argument inside another function because its an object.

**What are *args and *kwargs?****

*args(Non-Keyword Arguments/Positional Arguments) -> allow functions to accept any number of positional arguments i.e non-keyword arguments(key,value)

**kwargs(keyword arguments) -> any number of keyword arguments i.e key, vlaue pair argumets like dict.

**What is Scope in python?**

location where we define variable and in need we can access that.

Local Variable -> define in a function or in a loop

**What is docstring in Python?**

document string or docstring provide a convenient way of associating documentation with python modules,functions,classes and methods

”’triple single quotes”’ or “””triple double quotes”””

**What is Dynamically typed language?**

A language where data type assigned in run time via interpreted machine itself is called dynamically typed language.

**What is the difference between a shallow copy and a deep copy?**

shallow copy -> its create a new array or object but its not create a new copy instead of it points the object reference.

deep copy -> It creates the fully independent array with its new value but it is slow.

**What is Decorators?**

Decorator is a higher order function, which take another function as an argument and return a new function. this new function can alter or modify the original function.

**What is Iterators in Python?**

Iterator allow ietration on collections of data to like list, tuple, dict and set  means any kind of mutable data.

.iter() -> called to initialize the iterator. It must return an iterator object.

.next() -> called to iterate over the iterator. It must return the next value in the data stream.

**Iterator VS Iterable**

|                              | **Iterable** | **Iterator**                    |
| ---------------------------- | ------------------ | ------------------------------------- |
| **Iterated by using:** | for loop           | for loop                              |
| **Methods used:**      | __iter__()   | __iter__() and __next__() |

**What are generators in Python?**

In a function if there is one and more than one yield statement than that is generator.Yield keyword pause the execution of current line and save its state and afetr that start from there the execution start as per the requirement.

**What is Garbage collection in python?**

Process of automatic deletion of unwanted or unused object to free the memory we use garbage collection.

**What is zip function?**

The `zip()` function returns a zip object, which is an iterator of tuples where the first item in each passed iterator is paired together, and then the second item in each passed iterator are paired together etc.

**What are Pickling and Unpickling?**

Pickling is the process of converting python objects such as list, dictionaries, classes, or custom objects into a format that can be stored or transmitted efficiently. This serialized format is known as "pickle" or "pickled" object.

Unpickling means retrieve the serialized or pickled object and reconstruct it to its original format.

pickle.dump() -> for pickling the object

pickle.load() -> for unpickling the object

**What is self in code?**

It work's as a reference of instance for a class, and helps to access the variables that belongs to the class. We can write anythig instead of self, but inside a class in a function it always be the first parameter.

**What is Heap Memory?**

Heap memory is region of memory where python store it's objects aur data structures memory. It is nor organized in any format like stack or anything. Python used it to allocate memory.

**What is class and objects?**

In python everthing is object it can be method or any datatypes.

class is like a blueprint of object constructor where we build object.

**What is Namespaces in python?**

Namespace in python is like a container holds the identifier(name of variables, functions, classes etc) and map it with it's object name. It work like boundary for assuring that name must be unique and not get any conflict.

What is __init__?

`__init__` is a contructor method in Python and is automatically called to allocate memory when a new object/instance is created. All classes have a **__init__** method associated with them. It helps in distinguishing methods and attributes of a class from local variables.

What is the difference between Python Arrays and lists?

* Arrays in python can only contain elements of same data types i.e., data type of array should be homogeneous. It is a thin wrapper around C language arrays and consumes far less memory than lists.
* Lists in python can contain elements of different data types i.e., data type of lists can be heterogeneous. It has the disadvantage of
  consuming large memory.

---

**built-in data types in Python:**

**Immutable Data Types:**

1. int: Represents a whole number, such as 42 or -10.
2. float: Represents a decimal number, like 3.14 or -0.01.
3. complex: Comprises a real and an imaginary part, like 3 + 4j.
4. bool: Represents a boolean value, True or False.
5. str: A sequence of unicode characters enclosed within quotes.
6. tuple: An ordered collection of items, often heterogeneous, enclosed within parentheses.
7. frozenset: A set of unique, immutable objects, similar to sets, enclosed within curly braces.
8. bytes: Represents a group of 8-bit bytes, often used with binary data, enclosed within brackets.
9. bytearray: Resembles the 'bytes' type but allows mutable changes.
10. NoneType: Indicates the absence of a value.

**Mutable Data Types:**

1. list: A versatile ordered collection that can contain different data types and offers dynamic sizing, enclosed within square brackets.
2. set: Represents a unique set of objects and is characterized by curly braces.
3. dict: A versatile key-value paired collection enclosed within braces.
4. memoryview: Points to the memory used by another object, aiding efficient viewing and manipulation of data.
5. array: Offers storage for a specified type of data, similar to lists but with dedicated built-in functionalities.
6. deque: A double-ended queue distinguished by optimized insertion and removal operations from both its ends.
7. object: The base object from which all classes inherit.
8. types.SimpleNamespace: Grants the capability to assign attributes to it.
9. types.ModuleType: Represents a module body containing attributes.
10. types.FunctionType: Defines a particular kind of function.

**difference between a mutable and immutable object:**

| mutable                        | Immutable                         |
| ------------------------------ | --------------------------------- |
| Can be modified after creation | Cannot be modified after creation |
| Lists, Sets, Dictionaries      | Tuples, Strings, Numbers          |

**difference between list and  tuple:**

| List                                                                               | Tuple                                                       |
| ---------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| Lists are mutable                                                                  | Tuples are immutable                                        |
| The implication of iterations is Time-consuming                                    | The implication of iterations is comparatively Faster       |
| The list is better for performing operations, such as<br />insertion and deletion. | A Tuple data type is appropriate for accessing the elements |
| Lists consume more memory                                                          | Tuple consumes less memory as compared to the list          |
| Lists have several built-in methods                                                | Tuple does not have many built-in methods.                  |
| Unexpected changes and errors are more likely to occur                             | Because tuples don’t change they are far less error-prone. |

---

**LIST DATA TYPE:**

*Built-in List Functions & Methods:*

* len(list) -- Returns the total length of the list
* max(list) -- returns list's with the maximum or greatest value
* min(list) -- returns list's with the minimum or greatest value
* list(req) -- converts the tuple, dict and set etc into the list

List Methods:

* list.append(object) -- append object to the given list
* list.count(object) -- returns count of how many times the object occues in the list
* list.extend(sequence) -- appends the contents of sequence into the list
* list.index(object) -- give the least index in the list that the object appears
* list.insert(index,object) -- inserts object into the list at the offset index
* list.pop(object=list[-1) -- removes and returns the last object from the list
* list.remove(object) -- removes the object from the given list
* list.reverse() -- reverses objects of the list in the place
* list.sort([function]) -- sorts the objects of the list and use the compare function if its given

Difference Between append() and extend() in Python

| Append()                                                                                                   | Extend()                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| To add a single entry to the end of a list,<br />use the append() function.                                | To add additional elements or an iterable to the end of a list,<br />use the extend() function.                           |
| accepts only one input element.                                                                            | accepts as input an iterable (such as a list or tuple).                                                                   |
| The append() function adds the full input to the<br />list as a single item.                               | extend() adds each item to the list independently after iterating<br />through each one in the input.                     |
| Since append() only executes one operation, it is<br />typically quicker and more effective than extend(). | When adding elements from numerous iterables or with huge inputs,<br />extend() could take longer.                        |
| ****Append**** has constant time complexity i.e.,O(1)                                          | ****Extend**** has a time complexity of O(k). Where k is the length of the <br />list which need to be added. |

TUPLE Data Type:

* len(tup) -- it gives the total limit/length of the tuple
* max(tup) -- return maximum/greatest value
* min(tup) -- returns minimum/least value
* tuple(sequence) -- converts a list into the tuple
* [count()](https://www.w3schools.com/python/ref_tuple_count.asp) -- Returns the number of times a specified value occurs in a tuple
* [index()](https://www.w3schools.com/python/ref_tuple_index.asp) -- Searches the tuple for a specified value and returns the position of where it was found

DICTIONARY DATA TYPE:

* dict.clear() -- removes all the elements of the dict
* dict.copy() -- returns copy of dict
* dict.fromkeys() -- creates a new dict with the keys from the sequence and the values/items that are set to the value.
* dict.get(key,default=None) -- for key key, it returns the item/value or the default output if the respective key is not present in the dict.
* dict.has_key(key) -- returns true if the key is found or false
* dict.items() -- it returns a list of the given dictionary's (key,value) pair of the tuple
* dict.keys() -- returns the list of a dict keys
* dict.setdefault(key, default=none) -- similar to get(), but it will set the dict[key] = default if the key is not found in the given dict.
* dict.update(dict1) -- it adds the dictionary dict1's key-values pairs to the dict
* dict.values() -- it returns the list of the dict values
* dict(zip(keys, values)) -- The zip() function in Python is used to combine two or more iterable [dictionaries](https://www.geeksforgeeks.org/python-dictionary/) into a single iterable

THE SET DATA TYPE:

s1.add(element) -- adds element in s1

s1.union(s2) -- combines all the elements of both sets and returns them together

s1.intersection(s2) -- returns the elements which are common in both of the given sets.

s1.difference(s2) -- removes all elements of s2 that are present in s1 and then returns the rest elements of s1

s1.symmetric_difference(s2) -- removes all common elements of s1 and s2 and then returns rest of the elements together

s1==s2 -- returns true if boths the sets are symmetric

s1!=s2 -- returns true if both sets are not symmetric

s1<=s2 -- returns tru if the set s1 is the subset of set2

s1<s2 -- returns true if the set s1 is the proper/applicable subset of the set s2

s1>=s2 -- returns true if s2 is subset of s1

set.clear() -- removes all the elements of sets

set.remove() -- remove the specified elements from the set

set.copy() -- returns a copy of the respective set

frozenset(s1) -- returns true if s1 is forzenset

---

Difference between Generator and Normal Function:

| ****Scope**** | ****Generator****                                | ****Normal****                                          |
| ------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------------- |
| Execution                 | They can be paused in the middle of execution and resumed    | They runs to completion and returns a value                         |
| Return value              | They can return multiple values through multiple iterations. | They returns a single value (or none)                               |
| Memory usage              | They keeps the current value in memory,                      | They create a large amount of memory<br />overhead                  |
| Usage                     | They are used generate values that can be iterated over.     | They are used when to perform a task and<br />return a<br />result. |

---

1. Can we make set as a ordered set .
2. What is list compression and how it is different than lambda in python.

---

python follows a protocol to decide the scope of variable - LEGB(Local -> Enclosed -> Global -> Built-in).

**Local Scope:** when we declare a variable inside a function, it's a local variable, Its scope is limited to the function itself, means it can't be accessed outside of it.

**Enclosed Scope:** Enclosed scope refers to variables in the local scope of enclosing functions. This term becomes relevant when you have nested functions; where one function is wrapped inside another function.

**Global Scope:** global variables are variables defined outside all functions. python can recognize a global variable anywhere in the code be it inside or outside.

**Built-in Scope:** Built-in scope refers to names in Python’s built-in namespace, including all the built-in functions and types such as `str`, `list`, `dict`, `print()`, `len()`, etc. Python recognises these names anywhere in the code.

**Nested Functions:** function declared inside another function known as the ‘enclosing function’. These inner functions have access to the variables and names defined in the enclosing function.

```python
def outer_func():
    outer_var = 'I am in the outer function'
  
    def inner_func():
        inner_var = 'I am in inner function'
        print(outer_var)  # I can access outer_var
        print(inner_var)
 
    inner_func()

outer_func()
```

**Closures:** A closure is a nested function that remembers and has access to variables in the scope in which it was created, even if the outer function has finished execution.

```python
def outer_func(message):
    # This is the outer enclosing function

    def inner_func():
        # This is the nested function
        print(message)

    return inner_func  # Return without Parenthesis

my_func = outer_func("Hello World")
my_func()  # Output: "Hello World"
```

Free Variables: A free variable in Python is a variable used in a function that is not local or in the global scope. its part of the enclosing scope of the function.

```python
def outer_func(message):
    # Here, 'message' is a free variable
    def inner_func():
        print(message)
    return inner_func

my_func = outer_func("Hello World")
my_func()  # Output: "Hello World"

#message -> free variable

```

When and Why to Use Closures:

Data Hiding: Closures can be used to avoid the use of global values and provide some form of data hiding.

Function Factories: Closures can also be used to create function factories. A function factory is a function that returns a new function for each invocation, which can act on different data.

Lightweight, Anonymous Functions.

---

What is list comprehension and provide an example?

**Answer:**List comprehension is a concise way to create lists in Python.

```
squared_numbers = [x**2 for x in range(10)]
```

**Question:**
What is the difference between `==` and `is`?

**Answer:**
`==` checks for value equality, while `is` checks for identity (whether two references point to the same object in memory).

What are Python's magic (dunder) methods, and how are they used? Provide an example.

**Answer:**
Magic or dunder (double underscore) methods in Python are special methods that have double underscores at the beginning and end of their
names. They allow developers to emulate built-in behavior or implement operator overloading.

**Question:**
What is the difference between `__new__` and `__init__` in a class?

**Answer:**
`__new__` is responsible for creating and returning a new instance of the class, while `__init__` is responsible for initializing the created object.

What is the difference between an `Iterable` and an `Iterator`?

**Answer:**

* **Iterable** : An object which has an `__iter__` method that returns an iterator.
* **Iterator** : An object that can return its items one at a time using the `__next__` method and implements the `__iter__` method.

**32. Question:**
How does the `map` function work in Python?

**Answer:**
The `map` function applies a given function to all the items in an input list (or another iterable). For example:

What does the `zip` function do in Python?

**Answer:**
The `zip` function takes two or more iterables as argumentsand returns an iterator that generates tuples containing elements from the input iterables. Elements are paired based on their order.

names = ['Alice', 'Bob', 'Charlie']
ages = [25, 30, 35]
result = zip(names, ages)
print(list(result))  # Output: [('Alice', 25), ('Bob', 30), ('Charlie', 35)]

---

List: A list is a collection that is ordered and changeable. Allows duplicate members.

Tuple: Tuple is a collection that is ordered and unchangeable. Allows duplicate members.

Set:: Set is a collection that is unordered, unchangeable, and unindexed. No duplicate members.

Dictionary: A dictionary is a collection that is ordered and changeable. No duplicate members.

---

List Items:

* List items are ordered, changeable, and allow duplicate values.
* List items are indexed, the first item has an index[0], the second item has an index[1], etc.

---

Tuple: Tuple is the same as List except that it is immutable, i.e. once we create a tuple object, we cannot perform any changes in that object.

Tuple items are  **ordered** ,  **indexed** , **unchangeable,** and  **allow duplicate values** .

Since tuples are immutable, they do not have built-in methods like append(), extend(), insert(), remove(), etc. So if we are going to apply
these methods directly on tuples then it will throw an error.

But there are other ways to apply these functions on tuples, by directly converting tuples to lists and after updating values again converting
that list to tuples.

---

Sets

* Set is an unordered, unchangeable, unindexed collection and does not allow duplicates.Set items are unchangeable, but you can remove items and add new items means we can not update the set but can add or remove items.

The main difference between a set and a tuple is that in a set we can add or remove items but in the case of the tuple, once it’s created we
can not do anything on it.

Properties of sets:

Unordered, Unchangeable, Duplicates Not Allowed, Heterogeneous.

Why duplicates are not allowed in sets, and allowed in lists or tuples?

In the case of list or tuple they are indexed so, the index of duplicate item is different, and they are accessed by using an index, so duplicates are allowerd.But in the case of sets, there are no indexes so no duplicates members are allowed.

In list or tuple they are ordered meaning everything dependent on the index and hence duplicates are allowed, but in set everything is dependent on value and because it is unordered, that's why no duplicates members are allowed in sets.

If we use duplicates values in then it will not give an error but will print only one value and duplicates are not going to printed.

To access sets element there are three methods:

1. Using **in** keyword
2. Using **For loop**
3. Using **if-else** statements

Lists & Tuples Vs Set

* Wecan not use the update( ) method on a list or tuple, because there is no such method present for it, if we use then it will give an error.
* **We can use insert( ), append( ), extend( ) methods for lists or tuples but not for sets**
* **We can use add( ), and update( ) methods for sets but not for lists or tuples.**

frozenset: Frozenset is a set in which we can not do changes or do any updations in it.Python frozenset( ) Method creates an immutable Set object from an iterable. It is a built-in Python function.

---

Dictionary: A dictionary is an ordered, changeable collection and **does not allow duplicate keys. **Values can be duplicated but keys can not be duplicated****

Dictionary Properties

* A Python dictionary consists of a key and then an associated value. The value can be almost any Python object.
* Duplicate keys are not allowed but values can be duplicated.
* Heterogeneous objects are allowed for both keys and values.
* Dictionaries are mutable(can change or update values).
* Indexing and slicing concepts are not applicable.

Dictionary Items

* Dictionary items are **ordered, and changeable, and do not allow duplicate keys.**
* Dictionary items are presented in key: value pairs and can be referred to by using the key name.

Accessing dictionary items:

**Using keys, we can access values but using values we can not access keys**

1. Using square brackets and specifying the key name in it
2. Using the get( ) method by specifying the key name in it

Duplicate Keys Not Allowed:

* Dictionaries cannot have two items with the same key.
* If so, then it will consider the recent values of duplicates.
* **Dictionaries will not allow duplicates of keys**
* **Dictionaries will allow duplicates of values**

---

A function is a collection of related assertions that performs a mathematical, analytical, or evaluative operation.

Types of Functions

* Built-in Functions: function which are coming along with python software automatically, are called built-in or pre-defined functions. EX: id(), type(), input()
* user-defined functions: function which are developed by programmers.

Benefits/Advantages:

* larger code can be broken up into pieces.
* works on philosophy of write once use forever.
* code is organized and coherent.

Keywrod Use:

* def (mandaotry)
* return (optional)

Diff between return and print:

return will save the result of the output of a dunction as a variable.Print() will simply displays the output.

Function Arguments:

* Defualt Arguments: is kind of parameter that takes input a default vlue if not value is supplied for the argument when the function is called.
* Keyword Arguments: the parameter name and argument name must be the same.here order of argument is not important but the number of arguments must be matched.
* Required Arguments: also called positional arguments, tese are the arguments need to passed in the correct positional order. Number of parameters = number of arguments.
* Variable - length Arguments: we can use special characters in python functions to pass many arguments as we want in a function. There are two types of characters we can use:
  * *args: These are Non-Keyword Arguments
  * **kwargs: these are keyword arguments

Recursive Functions: when a function call itself is known as recursive(getting repeated again and again) function.

Advantages : reduce the length of code.

Lambda Function: is a small anonymous function. it can take any number of arguments, but can only have one expression.it is a one-liner dunction means we are giving defination, expression and arguments in one line.

Advantages: good for simple logical operations, good when ou want a function that you will use just one time.

Disadvantages: They can only perform one expression. It's not posiible to have multiple independent operations in one lambda function.

Diff between Lambda function and UDF function:

* there is only one expression in lambda function and there are n number of exceptions in UDF.
* we use lambda for lambda function for udf we use def.
* we can not call lambda function multiple time but we can call udf function may time.
* we use return keyword in udf but in lambda there is no need of return keyword.

Filter() Function - to filter values from the given sequence based on some condition.

map() Function - the function can be applied to each element of the sequence and generates a new sequence, ex: for every element present in the list perform a double and generates a new list of doubles.

reduce() function: reduces the sequence of elements into a single element by applying the specified function. available in functools module to use we have to import.

Enumerate Function: adds a counter to an iterable and returns it in a form of an enumerating object. this enumerated object can be directly used for loops or converted into a list using list() method. enumerate(iterable, start = 0)

---

Class: A class is a blueprint for creating objects, defining their attributes (data) and methods (functions). It encapsulates related data and behavior, providing a clear structure to work with.

Objects: Objects are instances of a class. They are created based on the class blueprint and can have their own unique data and behavior.

Inheritance: Inheritance allows us to create new classes based on existing ones, and allow classes to inherit common properties from the parent class.

Encapsulation: means it binds data and code together into one unit.

Polymorphism: is the ability to exist in many forms.

Abstraction: it displays only the important information by hiding the implementation part.


Diff between Abstraction and Encapsulation:

| Abstraction                                                                                                                                                      | Encapsulation                                                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Abstraction solve the problem in the design level.                                                                                                               | Encapsulation solves the problem in the implementation level.                                                                                                                                                      |
| Abstraction is used for hiding the unwanted data and giving relevant data.                                                                                       | Encapsulation means hiding the code and data into a single unit<br /> to protect the data from the outside world.                                                                                                  |
| Abstraction lets you focus on what the object does instead of how it does it.                                                                                    | Encapsulation means hiding the internal details or mechanics of<br />how an object does something.                                                                                                                 |
| Abstraction - outer layout, used in terms of design.<br />Ex: outer look of a mobile phone, like it has display screen and keypad buttons<br />to dial a number. | Encapuslation - Inner Layout , used in terms of implementation<br />EX: inner implementation details of a mobile phone, how keypad<br />button and display screen are connect with each other using <br />circuits |
