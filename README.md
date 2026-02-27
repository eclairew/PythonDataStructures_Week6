# Python Data Structures

## Lists

- We've now covered the simple variable types in Python: integers, floats, strings, and bools.
- However, there are several more complex types of variables that allow us to store and access multiple values.
- Perhaps the most versatile and common of these more complex types are lists.
- Lists are always specified using square brackets - `[]` (These are like vectors in R)
- Lists can contain an arbitrary number and type of simpler variables, but we often want to use only one type in a list so as not to get confused.
    - `listOfNums = [1,2,3,4]`
    - `listOfFloats = [3.14, 2.0, 12.3]`
    - `listOfStrings = ["Ecology", "Evolution", "Systematics"]`
    - `listOfBools = [True, False, False, True]`
- Even after they are created, lists can be modified. Individual elements can be added using the append method():
    - `listOfNums.append(5)` - Examine list after executing (append is a **method** here to the list function)
    - `listOfStrings.append("Neurobiology")`
- Elements can be removed using a few different methods.
    - Try `listOfFloats.pop()` - What is returned? And what does the list look like now? (This removes the last value in a list and returns the value that was removed)
    - You can remove specific values from a list, regardless of their position, by using the `remove(<VALUE>)` method. What happens when you execute `listOfBools.remove(False)`? How does the list change? (This requires you to specify the value and does not return the value that was removed)
- Lists can contain lists as elements (this way you can nest lists within larger lists, that list is then stored as a single value). For instance, try this:
    - `newList = []`
    - `newList.append([1,2,3])`
    - `newList.append([4,5,6])`
    - `newList.append([12,13,14])`
    - append only wants one thing at a time
- But you can also add all the _individual elements_ of one list to another. Try this:
    - `newList = [1,2,3]`
    - `newList.extend([4,5,6])`
    - `newList.extend([12,13,14])`
    - How does `newList` differ from what you got when you used `append()`?
- The following arguments will not modify the list object like the previously discussed methods:
-  You can view or extract parts of a list by using indices and "slicing" the list (just remember that python starts counting at 0!)
    - `newList[4:7]` - What values are returned? How do these relate to the indices you provided?
- You can also extract every n-th element of a list using notation like this:
    - `newList[::2]` - What values are returned now? (The third argument will specify an interval of which values to return, so here it will return every other value in the list)
    - `newList[2:8:2]` - How about now?
- You can also alter individual elements of lists by using indices
    - `newList`
    - `newList[2] = 100`
    - `newList`
- The method acts on the list it is given, you cannot assign it to a new list when using the method all in the same line
- If you set one list equal to another it is a shallow copy and those will always equal one another unless you use the copy method (which is a deep copy)

## `for` loops
  
- One of the nicest things about Python is the relationship between lists and `for` loops
- If you have an existing list, you can quickly iterate across all of its elements using this syntax:

```
for num in newList:
    print("This number is: %d" % num)
```
            
- If you still want to iterate over a series of integers, you can use the range() function.

```
for num in range(10):
    print("This number is: %d" % num)
```

## A note about "copying objects"

- Try this:
    - `firstNum = 2`
    - `secondNum = firstNum`
    - `firstNum = 5`
    - `firstNum`
    - `secondNum`
- Now try this:
    - `firstList = [1,2,3]`
    - `secondList = firstList`
    - `firstList.extend([4,5,6])`
    - `firstList`
    - `secondList`

## Tuples

- Tuples are like lists, but they're not mutable (can't be changed)
- Tuples are instantiated using parentheses - `()`
- Try this:
    - `myTuple = (1,2,3)`
    - `myTuple`
    - `myTuple[1]`
    - `myTuple[1] = 5`
    - Tuples have the count and index method but only because they are summarizing methods and not modifying methods.

## While loops

- Sometimes we want to do something repetitively, but we don't know ahead of time how many times we need to repeat it (as in a `for` loop.
- In these cases, we can use a `while` loop. A `while` loop will continue to do something until a certain condition is no longer satisfied.

```
num = 0
while num < 10:
    print(num)
    num += 1
```

- WARNING - You need to make sure to update variables such that the condition will eventually be satisified. If you don't, you could create an infinite loop!

## Dictionaries

- Dictionaries are incredibly useful for storing pairs of things - known as "keys" and "values"
- They don't store these pairs in a particular order, like lists do, but they make looking up values from keys much faster.
- The keys and values can each be different types of variables
- To create a new dictionary, you can use this syntax:
    - `myDict = {"keyOne":"valueOne", "keyTwo":"valueTwo"}`
- To look at the methods available for dictionaries, try this:
    - `dir(myDict)`
- You can access a value, as long as you know its key, either of these ways:
    - `myDict.get("keyOne")`
    - `myDict["keyOne"]`
- You can change a value using its key, this way:
    - `myDict["keyOne"] = <NEW_VALUE>`
- You can add a new key/value pair using the update method:
    - `myDict.update({<NEW_KEY:NEW_VALUE})`

## Reading from files

- To read or write from a file, you'll first need to define the file name
    - e.g., `inFileName = "FileToRead.txt"`
- However, this is just a string variable with the file name. We need to create an object that can actually read the contents of a file.
- Python has a built-in function to create a file object - `open(<FILENAME>,<MODE>)`
- The `<FILENAME>` argument is just a string with the file's name (or path to the file)
- The `<MODE>` argument tells Python whether we are reading from a file (`r`), writing to a file (`w`), or appending to a file (`a`).
- To open up a new File object to read file contents, use syntax like this:
    - `inFile = open(inFileName,'r')`
- There are several useful methods associated with file objects, but one of the most commonly used is `readline()`. This method will read lines one-by-one from the file. Note that the end of line character (\n) is retained when the line is read in.
    - `firstLine = inFile.readline()`
- Files opened for reading can be used in a `for` loop, as follows, to go through all the lines in the file:

```
        for line in file:
            print("Length of line is: %d" % (len(line)))
```

- Note that `line` is just a variable name we've chosen to hold each line as we iterate through the file. You can use any variable name you choose, as with any other `for` loop.


## Writing to Files

- Writing to a file is very similar to reading from a file. First, you define an output file name
    - `outFileName = "FileToWrite.txt"`
- To create a file object to use for writing, we'll again use the `open()` function, but we'll specify `'w'` for the `<MODE>`.
    - `outFile = open(outFileName,'w')`
- To write to the file line-by-line, we can use the `.write()` method.
    - `outFile.write("This is a new sentence.\n")`
    - Note that the `write()` method does NOT, by default, add a new line character to strings. If we want to end a line, we have to explicitly include `\n`.

## Importing libraries and drawing random numbers

- Sometimes it will be helpful to use functionality that's not part of the core python functionality.
- Thankfully, python has a built-in way to import new functions that other people have written to extend the core functions
- Once you know the name of a library, you can use the `import` command to load it (if it's already been installed).
- One library that we're going to use today is called `random`.
- Once it's loaded, you'll need to precede any of its functions with `random.` in order to use them.
- Try this:
    - `import random`
    - `random.random()` - Do this a few times
    - `random.uniform(0,1)` - Do this a few times
    - `random.uniform(0,5)` - Do this a few times
    - `random.choice([5,6,7,8])` - Do this a few times
    - `firstList`
    - `random.shuffle(firstList)`
    - `firstList`
    - `random.shuffle(firstList)`
    - `firstList`
    - `random.shuffle(firstList)`
    - `firstList`

## Command-line Arguments
  
- As with bash scripts, Python scripts can also take advantage of command-line arguments.
- To easily deal with command-line arguments, we're going to take advantage of some functions in the `sys` library. So we'll need to start by importing that library:
    - `import sys`
- Any command-line arguments we pass to a script can then be accessed using the `sys.argv` variable.
    - `print(sys.argv[2])`
    - Which argument is printed when you run the line above? Does that make sense with the 0-based indexing in Python?
- We can also loop through all command-line arguments:

```
        for arg in sys.argv:
            print(arg)
```

- These abilities are very useful in a variety of contexts, but particularly when a set of filenames are provided as command-line arguments and you want to iteratively process each file.

