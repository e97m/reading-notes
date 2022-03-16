# List Comprehensions

List comprehensions are a shortcut method that is easier and more readable which saves time for the developer and who read the code after him. The syntax is like: in `my_new_list` I want `expression` repeated using `for item in list`. The expression could be a variable, a variable multiplied by something, a tuple, a function, etc... 

```Python:
my_new_list = [ expression for item in list ]
```

it’s possible to add conditional statements in the form of filters, which allows for more precision in the way lists are handled;

```Python:
my_new_list = [ expression for item in list if condition ]
```

it’s also possible to add nested loops, in comprehensions:

```Python:
my_new_list = [ expression for item in list for item2 in list2 ]
```

<br>

## Examples:

### Normal case

```Python:
digits = [x for x in range(10)]
>>> [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

```Python:
squares = [x**2 for x in range(10)]
>>> [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

```Python:
authors = ["Ernest Hemingway","Langston Hughes","Frank Herbert","Toni Morrison", "Emily Dickson","Stephen King"]
letters = [ name[0] for name in authors ]
>>>['E', 'L', 'F', 'T', 'E', 'S']
```

```Python:
letters = [ letter for letter in "20,000 Leagues Under The Sea"]
>>> ['2', '0', ',', '0', '0', '0', ' ', 'L', 'e', 'a', 'g', 'u', 'e', 's', ' ', 'U', 'n', 'd', 'e', 'r', ' ', 'T', 'h', 'e', ' ', 'S', 'e', 'a']
```

```Python:
lower_case = [ letter.lower() for letter in ['A','B','C'] ]
>>> ['a', 'b', 'c']
```

```Python:
file = open("dreams.txt", 'r')
poem = [ line for line in file ]
```

```Python:
nums = [double(x) for x in range(1,10)]
>>> [2, 4, 6, 8, 10, 12, 14, 16, 18]
```

<br>

### Conditional case

```Python:
even_numbers = [ x for x in range(1,20) if x % 2 == 0]
>>> [2, 4, 6, 8, 10, 12, 14, 16, 18]
```

```Python:
user_data = "Elvis Presley 987-654-3210"
phone_number = [ x for x in user_data if x.isdigit()]
>>> ['9', '8', '7', '6', '5', '4', '3', '2', '1', '0']
```

<br>

### Nested case:

```Python:
nums = [x+y for x in [1,2,3] for y in [10,20,30]]
>>> [11, 21, 31, 12, 22, 32, 13, 23, 33]
```

```Python:
nums = [(x,y) for x in [1,2,3] for y in [10,20,30]]
>>> [(1, 10), (2, 20), (3, 30)]
```