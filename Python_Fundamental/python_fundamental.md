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
| **Example**        | my_set = {1, 2, 3}                          | my_dict = {“name”: “Alice”, “age”: 30}<br />    |

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
