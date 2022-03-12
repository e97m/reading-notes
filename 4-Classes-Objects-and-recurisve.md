# Claases and Objects

Objects are an encapsulation of variables and functions into a single entity. Objects get their variables and functions from classes. Classes are essentially a template to create your objects.

The following example shows that the variable "myobjectx" holds an object of the class "MyClass" that contains the variable and the function defined within the class called "MyClass".

    class MyClass:
        variable = "blah"

        def function(self):
            print("This is a message inside the class.")

    myobjectx = MyClass()

To access the variable inside of the newly created object in the previous example you cold use `myobjectx.variable`. And the same for functions `myobjectx.function()`.

As you can see, every function inside the class has to have at least one parameter `(self)`.

You can create multiple different objects that are of the same class(have the same variables and functions defined). However, each object contains independent copies of the variables defined in the class. for example `myobjectx = MyClass()` and
`myobjecty = MyClass()`.

The `__init__()` function, is a special function that is called when the class is being initiated. It's used for assigning values in a class.

    class NumberHolder:

        def __init__(self, number):
             self.number = number



<br>

<br>

# Thinking Recursively in Python

A recursive function is a function defined in terms of itself via self-referential expressions. This means that the function will continue to call itself and repeat its behavior until some condition is met to return a result. All recursive functions share a common structure made up of two parts: base case and recursive case. For example n! could be written as a recursive function.

    def factorial_recursive(n):
        if n == 1:
            return 1
        else:
            return n * factorial_recursive(n-1)

<br>

## Maintaining State

When dealing with recursive functions, keep in mind that each recursive call has its own execution context, so to maintain state during recursion you have to either:

- Thread the state through each recursive call so that the current state is part of the current call’s execution context
- Keep the state in global scope

<br>

    current_number = 1
    accumulated_sum = 0

    def sum_recursive():
        global current_number
        global accumulated_sum

        if current_number == 11:
            return accumulated_sum
        else:
            accumulated_sum = accumulated_sum + current_number
            current_number = current_number + 1
            return sum_recursive()


<br>

## Recursive Data Structures in Python

A data structure is recursive if it can be deﬁned in terms of a smaller version of itself. A list is an example of a recursive data structure. Let me demonstrate.

    def attach_head(element, input_list):
        return [element] + input_list

    attach_head(1, attach_head(46,attach_head(-31, attach_head("hello", []))))

Output -->  [1, 46, -31, 'hello']

Recursion can also be seen as self-referential function composition. We apply a function to an argument, then pass that result on as an argument to a second application of the same function, and so on.

The recursive function’s structure can often be modeled after the definition of the recursive data structure it takes as an input. For example, calculating the sum of all the elements of a list recursively:

    def list_sum_recursive(input_list):
        # Base case
        if input_list == []:
            return 0

        # Recursive case
        # Decompose the original problem into simpler instances of the same problem
        # by making use of the fact that the input is a recursive data structure
        # and can be deﬁned in terms of a smaller version of itself
        else:
            head = input_list[0]
            smaller_list = input_list[1:]
            return head + list_sum_recursive(smaller_list)


<br>

<br>

# I recommend you to read about [Naive Recursion](https://realpython.com/python-thinking-recursively/)