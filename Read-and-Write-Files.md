# Read and Write Files

File is At its core, a file is a contiguous set of bytes used to store data. Files on most modern file systems are composed of three main parts:

1. Header: metadata about the contents of the file (file name, size, type, and so on)
2. Data: contents of the file as written by the creator or editor
3. End of file (EOF): special character that indicates the end of the file

The file path is broken up into three major parts:
1. Folder Path: the file folder location on the file system where subsequent folders are separated by a forward slash / (Unix) or backslash \ (Windows)
2. File Name: the actual name of the file
3. Extension: the end of the file path pre-pended with a period (.) used to indicate the file type.

ASA standard states that line endings should use the sequence of the Carriage Return (CR or \r) and the Line Feed (LF or \n) characters (CR+LF or \r\n). The ISO standard however allowed for either the CR+LF characters or just the LF character.

The two most common encodings are the ASCII and UNICODE Formats. ASCII can only store 128 characters, while Unicode can contain up to 1,114,112 characters. ASCII is actually a subset of Unicode (UTF-8), meaning that ASCII and Unicode share the same numerical to character values. But that don't prevent parsing a file with the incorrect character encoding to lead to failures or misrepresentation of the character, so be carful.

<br>

<br>

## Opening and Closing a File in Python

`open()` has a single required argument that is the path to the file. `open()` has a single return, the file object. It’s important to remember that it’s your responsibility to close the file.

The first way to close a file is to use the `try`-`finally` block:

>reader = open('dog_breeds.txt' , 'r')
>
>try:
>> \# Further file processing goes here
>
>finally:
>> reader.close()

The second way to close a file is to use the `with` statement:

>with open('dog_breeds.txt' , 'r') as reader:
>> \# Further file processing goes here
>
> \#File is closed here even in cases of error

<br>

The most commonly used options with open:
- `r`: Open for reading (default)
- `w` : Open for writing, truncating (overwriting) the file first
- `rb` or `wb` : Open in binary mode (read/write using byte data)

<br>

A file object is an object exposing a file-oriented API (with methods such as `read()` or `write()`) to an underlying resource. categories of file objects: Text files, Buffered binary files, and Raw binary files. Each of these file types are defined in the io module. 

<br>

<br>

## Reading and Writing Opened Files

There are multiple methods that read a file:
- `.read(size=-1)` : This reads from the file based on the number of size bytes. If no argument is passed or None or -1 is passed, then the entire file is read.
- `.readline(size=-1)` : This reads at most size number of characters from the line. This continues to the end of the line and then wraps back around. If no argument is passed or None or -1 is passed, then the entire line (or rest of the line) is read.
- `.readlines()` : This reads the remaining lines from the file object and returns them as a list.

<br>

## Iterating Over Each Line in the File

Dont forget to print after you read if you want to test reading command (it is common to do so)

>with open('dog_breeds.txt', 'r') as reader:
>> line = reader.readline()
>>
>> while line != "": 
>>> print(line, end="")
>>>
>>> line = reader.readline()

or

> with open('dog_breeds.txt', 'r') as reader:
>> for line in reader:
>>>  print(line, end='')

<br>

File objects have multiple methods that are useful for writing to a file:

-  `.write(string)` : This writes the string to the file.
- `.writelines(seq)` : This writes the sequence to the file. No line endings are appended to each sequence item. It’s up to you to add the appropriate line ending(s).

>with open('dog_breeds_reversed.txt', 'w') as writer:
>> writer.writelines(reversed(dog_breeds))

or

> with open('dog_breeds_reversed.txt', 'w') as writer:
>> for breed in reversed(dog_breeds):
>>> writer.write(breed)

<br>

<br>

## Working With Bytes

Sometimes, you may need to work with files using byte strings. This is done by adding the 'b' character to the mode argument. All of the same methods for the file object apply. However, each of the methods expect and return a bytes object instead:

<br>

## Tips and Tricks

### `__file__`  :

The `__file__` attribute is a special attribute of modules, similar to `__name__`. It is the pathname of the file from which the module was loaded, if it was loaded from a file.

<br>

### Appending to a File:

Sometimes, you may want to append to a file or start writing at the end of an already populated file. This is easily done by using the 'a' character for the mode argument:

>with open('dog_breeds.txt', 'a') as a_writer:
>>a_writer.write('\nBeagle')

<br>

### Working With Two Files at the Same Time:

> d_path = 'dog_breeds.txt'
>
> d_r_path = 'dog_breeds_reversed.txt'
>
> with open(d_path, 'r') as reader, open(d_r_path, 'w') as writer:
>> dog_breeds = reader.readlines()
>> writer.writelines(reversed(dog_breeds))

<br>

### Creating Your Own Context Manager:

There may come a time when you’ll need finer control of the file object by placing it inside a custom class. When you do this, using the with statement can no longer be used unless you add a few magic methods: __enter__ and __exit__. By adding these, you’ll have created what’s called a context manager.


<br>

<br>

<br>

# For more read [this article](https://realpython.com/read-write-files-python/)