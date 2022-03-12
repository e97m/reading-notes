# Read/Write and Exceptions in Python

## Exceptions:

`Syntax errors` occur when the parser detects an incorrect statement. `Exception error` occurs whenever the syntactically correct Python code results an error. Their are a lot of built-in exceptions in Python, for example, `ZeroDivisionError`, `NameError`, `TypeError`, `ValueError`, and `AssertionError`.

However, we can use `raise` to throw an exception if a condition occurs. The statement can be complemented with a custom exception.

>x = 10
>
> if x > 5:
>
>> raise Exception('x should not exceed 5. The value of x was: {}'.format(x))

***AssertionError*** : Instead of waiting for a program to crash midway, you can also start by making an assertion in Python. We `assert` that a certain condition is met. If this condition turns out to be True, then that is excellent! The program can continue. If the condition turns out to be False, you can have the program throw an `AssertionError` exception.

> import sys
>
>assert ('linux' in sys.platform), "This code runs on Linux only."

<br>

## Handling Exceptions:

The `try` and `except` block in Python is used to catch and handle exceptions. Python executes code following the `try` statement as a “normal” part of the program. The code that follows the `except` statement is the program’s response to any exceptions in the preceding `try` clause.

>def linux_interaction():
>> assert ('linux' in sys.platform), "Function can only run on Linux systems."
>>
>> print('Doing something.')
>
>try:
>> linux_interaction()
>
>except:
>> print('Linux function was not executed')

The example above doesn't print anything, you can print a message to explain more. But in this case, it is recommended to specify the error type that you want to print that comment when it occurs. BTW you can also add more than one exception and specify a different attitude for every one of them.

>def linux_interaction():
>> assert ('linux' in sys.platform), "Function can only run on Linux systems."
>>
>> print('Doing something.')
>
>try:
>> linux_interaction()
>>
>> with open('file.log') as file:
>>> read_data = file.read()
>
> except AssertionError as error:
>> print(error)
>>
>> print('The linux_interaction() function was not executed')
>
> except FileNotFoundError as fnf_error:
>> print(fnf_error)

Output : Function can only run on Linux systems.
The linux_interaction() function was not executed. /// or /// Output: [Errno 2] No such file or directory: 'file.log'

## The else Clause

In Python, using the else statement, you can instruct a program to execute a certain block of code only in the absence of exceptions. You can also try to run code inside the else clause and catch possible exceptions there as well:

>def linux_interaction():
>> assert ('linux' in sys.platform), "Function can only run on Linux systems."
>>
>> print('Doing something.')
>
>try:
>> linux_interaction()
>
>except AssertionError as error:
>> print(error)
>
> else:
>> try:
>>> with open('file.log') as file:
>>>> read_data = file.read()
>>>
>>> except FileNotFoundError as fnf_error:
>>>> print(fnf_error)

Output: Doing something.
[Errno 2] No such file or directory: 'file.log'

<br>

## Cleaning Up After Using finally

Imagine that you always had to implement some sort of action to clean up after executing your code. Python enables you to do so using the finally clause.

<br>

## Summing Up

After seeing the difference between syntax errors and exceptions, you learned about various ways to raise, catch, and handle exceptions in Python. In this article, you saw the following options:

- `raise` allows you to throw an exception at any time.
- `assert` enables you to verify if a certain condition is met and throw an exception if it isn’t.
- In the `try` clause, all statements are executed until an exception is encountered.
- `except` is used to catch and handle the exception(s) that are encountered in the try clause.
- `else` lets you code sections that should run only when no exceptions are encountered in the try clause.
- `finally` enables you to execute sections of code that should always run, with or without any previously encountered exceptions.
