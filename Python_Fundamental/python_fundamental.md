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
