# Test Driven Development (TDD)

Its a method to test the code before deploying it by repeatedly testing the software against all test cases.

TDD cicle:
1. Add a test
2. Run all tests. The new test should fail for expected reasons
3. Write the simplest code that passes the new test
4. All tests should now pass
5. Refactor as needed, using tests after each refactor to ensure that functionality is preserved
6. Repeat for each new piece of functionality

<br>

# main and name

If the python interpreter is running a module (the source file) as the main program, it sets the special `__ name __ `variable to have a value `__ main __` . If this file is being imported from another module, `__ name __` will be set to the module’s name. Module’s name is available as value to `__ name __` global variable. This let us control what to import from moduls.

<br>

# Recursion

Is a process in which a function calls itself directly or indirectly, recursion could also be two functions calling each other until a base case. A recursive function is tail recursive when recursive call is the last thing executed by the function. 

When any function is called, the memory is allocated to it on the stack. A recursive function calls itself, the memory for a called function is allocated on top of memory allocated to calling function and different copy of local variables is created for each function call. When the base case is reached, the function returns its value to the function by whom it is called and memory is de-allocated and the process continues.