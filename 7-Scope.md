# Scope

The concept of scope rules how variables and names are looked up in your code. It determines the visibility of a variable within the code. The scope of a name or variable depends on the place in your code where you create that variable.

Most common scopes:

- Global scope: The names that you define in this scope are available to all your code.
- Local scope: The names that you define in this scope are only available or visible to the code within the scope.

You’ll be using the term name to refer to the identifiers of variables, constants, functions, classes, or any other object that can be assigned a name. The names in your programs will have the scope of the block of code in which you define them. Where you assign or define a name in your code determines the scope or visibility of that name.

 Python scopes are implemented as dictionaries that map names to objects. These dictionaries are commonly called namespaces. These are the concrete mechanisms that Python uses to store names. They’re stored in a special attribute called .__dict__. Names at the top level of a module are stored in the module’s namespace. In other words, they’re stored in the module’s .__dict__ attribute. `sys.__dict__.keys()` or `module.__dict__['name']` will return a list of the name in the global scope.

<br>

## LEGB Rule

- ***Local (or function) scope*** is the code block or body of any Python function or lambda expression. This Python scope contains the names that you define inside the function. These names will only be visible from the code of the function. It’s created at function call, not at function definition, so you’ll have as many different local scopes as function calls. This is true even if you call the same function multiple times, or recursively. Each call will result in a new local scope being created.

- ***Enclosing (or nonlocal) scope*** is a special scope that only exists for nested functions. If the local scope is an inner or nested function, then the enclosing scope is the scope of the outer or enclosing function. This scope contains the names that you define in the enclosing function. The names in the enclosing scope are visible from the code of the inner and enclosing functions.

- ***Global (or module) scope*** is the top-most scope in a Python program, script, or module. This Python scope contains all of the names that you define at the top level of a program or a module. Names in this Python scope are visible from everywhere in your code.

- ***Built-in scope*** is a special Python scope that’s created or loaded whenever you run a script or open an interactive session. This scope contains names such as keywords, functions, exceptions, and other attributes that are built into Python. Names in this Python scope are also available from everywhere in your code. It’s automatically loaded by Python when you run a program or script.