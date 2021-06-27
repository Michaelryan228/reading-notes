The concept of scope rules how variables and names are looked up in your code. It determines the visibility of a variable within the code. The scope of a name or variable depends on the place in your code where you create that variable. The Python scope concept is generally presented using a rule known as the LEGB rule.

The letters in the acronym LEGB stand for Local, Enclosing, Global, and Built-in scopes. This summarizes not only the Python scope levels but also the sequence of steps that Python follows when resolving names in a program.

In this tutorial, you’ll learn:

What scopes are and how they work in Python
Why it’s important to know about Python scope
What the LEGB rule is and how Python uses it to resolve names
How to modify the standard behavior of Python scope using global and nonlocal
What scope-related tools Python offers and how you can use them
With this knowledge at hand, you can take advantage of Python scopes to write more reliable and maintainable programs. Using Python scope will help you avoid or minimize bugs related to name collision as well as bad use of global names across your programs.

You’ll get the most out of this tutorial if you’re familiar with intermediate Python concepts like classes, functions, inner functions, variables, exceptions, comprehensions, built-in functions, and standard data structures.

Understanding Scope
In programming, the scope of a name defines the area of a program in which you can unambiguously access that name, such as variables, functions, objects, and so on. A name will only be visible to and accessible by the code in its scope. Several programming languages take advantage of scope for avoiding name collisions and unpredictable behaviors. Most commonly, you’ll distinguish two general scopes:

Global scope: The names that you define in this scope are available to all your code.

Local scope: The names that you define in this scope are only available or visible to the code within the scope.

Scope came about because early programming languages (like BASIC) only had global names. With this kind of name, any part of the program could modify any variable at any time, so maintaining and debugging large programs could become a real nightmare. To work with global names, you’d need to keep all the code in mind at the same time to know what the value of a given name is at any time. This was an important side-effect of not having scopes.

Some languages like Python use scope to avoid this kind of problem. When you use a language that implements scope, there’s no way for you to access all the variables in a program at all locations in that program. In this case, your ability to access a given name will depend on where you’ve defined that name.

Note: You’ll be using the term name to refer to the identifiers of variables, constants, functions, classes, or any other object that can be assigned a name.

The names in your programs will have the scope of the block of code in which you define them. When you can access the value of a given name from someplace in your code, you’ll say that the name is in scope. If you can’t access the name, then you’ll say that the name is out of scope.

Names and Scopes in Python
Since Python is a dynamically-typed language, variables in Python come into existence when you first assign them a value. On the other hand, functions and classes are available after you define them using def or class, respectively. Finally, modules exist after you import them. As a summary, you can create Python names through one of the following operations:

Operation	Statement
Assignments	x = value
Import operations	import module or from module import name
Function definitions	def my_func(): ...
Argument definitions in the context of functions	def my_func(arg1, arg2,... argN): ...
Class definitions	class MyClass: ...
All these operations create or, in the case of assignments, update new Python names because all of them assign a name to a variable, constant, function, class, instance, module, or other Python object.

Note: There’s an important difference between assignment operations and reference or access operations. When you reference a name, you’re just retrieving its content or value. When you assign a name, you’re either creating that name or modifying it.

Python uses the location of the name assignment or definition to associate it with a particular scope. In other words, where you assign or define a name in your code determines the scope or visibility of that name.

For example, if you assign a value to a name inside a function, then that name will have a local Python scope. In contrast, if you assign a value to a name outside of all functions—say, at the top level of a module—then that name will have a global Python scope.

Python Scope vs Namespace
In Python, the concept of scope is closely related to the concept of the namespace. As you’ve learned so far, a Python scope determines where in your program a name is visible. Python scopes are implemented as dictionaries that map names to objects. These dictionaries are commonly called namespaces. These are the concrete mechanisms that Python uses to store names. They’re stored in a special attribute called .__dict__.

Names at the top level of a module are stored in the module’s namespace. In other words, they’re stored in the module’s .__dict__ attribute. Take a look at the following code:

>>> import sys
>>> sys.__dict__.keys()
dict_keys(['__name__', '__doc__', '__package__',..., 'argv', 'ps1', 'ps2'])
After you import sys, you can use .keys() to inspect the keys of sys.__dict__. This returns a list with all the names defined at the top level of the module. In this case, you can say that .__dict__ holds the namespace of sys and is a concrete representation of the module scope.

Note: The output of some of the examples in this tutorial has been abbreviated (...) to save space. The output may vary based on your platform, Python version, or even on how long you’ve been using your current Python interactive session.

As a further example, suppose that you need to use the name ps1, which is defined in sys. If you know how .__dict__ and namespaces work in Python, then you can reference ps1 in at least two different ways:

Using the dot notation on the module’s name in the form module.name
Using a subscription operation on .__dict__ in the form module.__dict__['name']
Take a look at the following code:

>>> sys.ps1
'>>> '
>>> sys.__dict__['ps1']
'>>> '
Once you’ve imported sys you can access ps1 using the dot notation on sys. You can also access ps1 using a dictionary key lookup with the key 'ps1'. Both actions return the same result, '>>> '.

Note: ps1 is a string specifying the primary prompt of the Python interpreter. ps1 is only defined if the interpreter is in interactive mode and its initial value is '>>> '.

Whenever you use a name, such as a variable or a function name, Python searches through different scope levels (or namespaces) to determine whether the name exists or not. If the name exists, then you’ll always get the first occurrence of it. Otherwise, you’ll get an error. You’ll cover this search mechanism in the next section.

Using the LEGB Rule for Python Scope
Python resolves names using the so-called LEGB rule, which is named after the Python scope for names. The letters in LEGB stand for Local, Enclosing, Global, and Built-in. Here’s a quick overview of what these terms mean:

Local (or function) scope is the code block or body of any Python function or lambda expression. This Python scope contains the names that you define inside the function. These names will only be visible from the code of the function. It’s created at function call, not at function definition, so you’ll have as many different local scopes as function calls. This is true even if you call the same function multiple times, or recursively. Each call will result in a new local scope being created.

Enclosing (or nonlocal) scope is a special scope that only exists for nested functions. If the local scope is an inner or nested function, then the enclosing scope is the scope of the outer or enclosing function. This scope contains the names that you define in the enclosing function. The names in the enclosing scope are visible from the code of the inner and enclosing functions.

Global (or module) scope is the top-most scope in a Python program, script, or module. This Python scope contains all of the names that you define at the top level of a program or a module. Names in this Python scope are visible from everywhere in your code.

Built-in scope is a special Python scope that’s created or loaded whenever you run a script or open an interactive session. This scope contains names such as keywords, functions, exceptions, and other attributes that are built into Python. Names in this Python scope are also available from everywhere in your code. It’s automatically loaded by Python when you run a program or script.

The LEGB rule is a kind of name lookup procedure, which determines the order in which Python looks up names. For example, if you reference a given name, then Python will look that name up sequentially in the local, enclosing, global, and built-in scope. If the name exists, then you’ll get the first occurrence of it. Otherwise, you’ll get an error.

Note: Notice that the local and enclosing Python scopes are searched only if you use a name inside a function (local scope) or a nested or inner function (local and enclosing scope).

In summary, when you use nested functions, names are resolved by first checking the local scope or the innermost function’s local scope. Then, Python looks at all enclosing scopes of outer functions from the innermost scope to the outermost scope. If no match is found, then Python looks at the global and built-in scopes. If it can’t find the name, then you’ll get an error.

At any given time during execution, you’ll have at most four active Python scopes—local, enclosing, global, and built-in—depending on where you are in the code. On the other hand, you’ll always have at least two active scopes, which are the global and built-in scopes. These two scopes will always be available for you.

Functions: The Local Scope
The local scope or function scope is a Python scope created at function calls. Every time you call a function, you’re also creating a new local scope. On the other hand, you can think of each def statement and lambda expression as a blueprint for new local scopes. These local scopes will come into existence whenever you call the function at hand.

By default, parameters and names that you assign inside a function exist only within the function or local scope associated with the function call. When the function returns, the local scope is destroyed and the names are forgotten. Here’s how this works:

>>> def square(base):
...     result = base ** 2
...     print(f'The square of {base} is: {result}')
...
>>> square(10)
The square of 10 is: 100
>>> result  # Isn't accessible from outside square()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
    result
NameError: name 'result' is not defined
>>> base  # Isn't accessible from outside square()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
    base
NameError: name 'base' is not defined
>>> square(20)
The square of 20 is: 400
square() is a function that computes the square of a given number, base. When you call the function, Python creates a local scope containing the names base (an argument) and result (a local variable). After the first call to square(), base holds a value of 10 and result holds a value of 100. The second time, the local names will not remember the values that were stored in them the first time the function was called. Notice that base now holds the value 20 and result holds 400.

Note: If you try to access result or base after the function call, then you get a NameError, because these only exist in the local scope created by the call to square(). Whenever you try to access a name that isn’t defined in any Python scope, you’ll get a NameError. The error message will include the name that couldn’t be found.

Since you can’t access local names from statements that are outside the function, different functions can define objects with the same name. Check out this example:

>>> def cube(base):
...     result = base ** 3
...     print(f'The cube of {base} is: {result}')
...
>>> cube(30)
The cube of 30 is: 27000
Notice that you define cube() using the same variable and parameter that you used in square(). However, since cube() can’t see the names inside the local scope of square() and vice versa, both functions work as expected without any name collision.

You can avoid name collisions in your programs by properly using the local Python scope. This also makes functions more self-contained and creates maintainable program units. Additionally, since you can’t change local names from remote places in your code, your programs will be easier to debug, read, and modify.

You can inspect the names and parameters of a function using .__code__, which is an attribute that holds information on the function’s internal code. Take a look at the code below:

>>> square.__code__.co_varnames
('base', 'result')
>>> square.__code__.co_argcount
1
>>> square.__code__.co_consts
(None, 2, 'The square of ', ' is: ')
>>> square.__code__.co_name
'square'
In this code example, you inspect .__code__ on square(). This is a special attribute that holds information about the code of a Python function. In this case, you see that .co_varnames holds a tuple containing the names that you define inside square().

Nested Functions: The Enclosing Scope
Enclosing or nonlocal scope is observed when you nest functions inside other functions. The enclosing scope was added in Python 2.2. It takes the form of the local scope of any enclosing function’s local scopes. Names that you define in the enclosing Python scope are commonly known as nonlocal names. Consider the following code:

>>> def outer_func():
...     # This block is the Local scope of outer_func()
...     var = 100  # A nonlocal var
...     # It's also the enclosing scope of inner_func()
...     def inner_func():
...         # This block is the Local scope of inner_func()
...         print(f"Printing var from inner_func(): {var}")
...
...     inner_func()
...     print(f"Printing var from outer_func(): {var}")
...
>>> outer_func()
Printing var from inner_func(): 100
Printing var from outer_func(): 100
>>> inner_func()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'inner_func' is not defined
When you call outer_func(), you’re also creating a local scope. The local scope of outer_func() is, at the same time, the enclosing scope of inner_func(). From inside inner_func(), this scope is neither the global scope nor the local scope. It’s a special scope that lies in between those two scopes and is known as the enclosing scope.

Note: In a sense, inner_func() is a temporary function that comes to life only during the execution of its enclosing function, outer_func(). Note that inner_func() is only visible to the code in outer_func().

All the names that you create in the enclosing scope are visible from inside inner_func(), except for those created after you call inner_func(). Here’s a new version of outer_fun() that shows this point:

>>> def outer_func():
...     var = 100
...     def inner_func():
...         print(f"Printing var from inner_func(): {var}")
...         print(f"Printing another_var from inner_func(): {another_var}")
...
...     inner_func()
...     another_var = 200  # This is defined after calling inner_func()
...     print(f"Printing var from outer_func(): {var}")
...
>>> outer_func()
Printing var from inner_func(): 100
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
    outer_func()
  File "<stdin>", line 7, in outer_func
    inner_func()
  File "<stdin>", line 5, in inner_func
    print(f"Printing another_var from inner_func(): {another_var}")
NameError: free variable 'another_var' referenced before assignment in enclosing
 scope
When you call outer_func() the code runs down to the point in which you call inner_func(). The last statement of inner_func() tries to access another_var. At this point, another_var isn’t defined yet, so Python raises a NameError because it can’t find the name that you’re trying to use.

Last but not least, you can’t modify names in the enclosing scope from inside a nested function unless you declare them as nonlocal in the nested function. You’ll cover how to use nonlocal later in this tutorial.

Modules: The Global Scope
From the moment you start a Python program, you’re in the global Python scope. Internally, Python turns your program’s main script into a module called __main__ to hold the main program’s execution. The namespace of this module is the main global scope of your program.

Note: In Python, the notions of global scope and global names are tightly associated with module files. For example, if you define a name at the top level of any Python module, then that name is considered global to the module. That’s the reason why this kind of scope is also called module scope.

If you’re working in a Python interactive session, then you’ll notice that '__main__' is also the name of its main module. To check that out, open an interactive session and type in the following:

>>> __name__
'__main__'
Whenever you run a Python program or an interactive session like in the above code, the interpreter executes the code in the module or script that serves as an entry point to your program. This module or script is loaded with the special name, __main__. From this point on, you can say that your main global scope is the scope of __main__.

To inspect the names within your main global scope, you can use dir(). If you call dir() without arguments, then you’ll get the list of names that live in your current global scope. Take a look at this code:

>>> dir()
['__annotations__', '__builtins__',..., '__package__', '__spec__']
>>> var = 100  # Assign var at the top level of __main__
>>> dir()
['__annotations__', '__builtins__',..., '__package__', '__spec__', 'var']
When you call dir() with no arguments, you get the list of names available in your main global Python scope. Note that if you assign a new name (like var here) at the top level of the module (which is __main__ here), then that name will be added to the list returned by dir().

Note: You’ll cover dir() in more detail later on in this tutorial.

There’s only one global Python scope per program execution. This scope remains in existence until the program terminates and all its names are forgotten. Otherwise, the next time you were to run the program, the names would remember their values from the previous run.

You can access or reference the value of any global name from any place in your code. This includes functions and classes. Here’s an example that clarifies these points:

>>> var = 100
>>> def func():
...     return var  # You can access var from inside func()
...
>>> func()
100
>>> var  # Remains unchanged
100
Inside func(), you can freely access or reference the value of var. This has no effect on your global name var, but it shows you that var can be freely accessed from within func(). On the other hand, you can’t assign global names inside functions unless you explicitly declare them as global names using a global statement, which you’ll see later on.

Whenever you assign a value to a name in Python, one of two things can happen:

You create a new name
You update an existing name
The concrete behavior will depend on the Python scope in which you’re assigning the name. If you try to assign a value to a global name inside a function, then you’ll be creating that name in the function’s local scope, shadowing or overriding the global name. This means that you won’t be able to change most variables that have been defined outside the function from within the function.

If you follow this logic, then you’ll realize that the following code won’t work as you might expect:

>>> var = 100  # A global variable
>>> def increment():
...     var = var + 1  # Try to update a global variable
...
>>> increment()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
    increment()
  File "<stdin>", line 2, in increment
    var = var + 1
UnboundLocalError: local variable 'var' referenced before assignment
Within increment(), you try to increment the global variable, var. Since var isn’t declared global inside increment(), Python creates a new local variable with the same name, var, inside the function. In the process, Python realizes that you’re trying to use the local var before its first assignment (var + 1), so it raises an UnboundLocalError.

Here’s another example:

>>> var = 100  # A global variable
>>> def func():
...     print(var)  # Reference the global variable, var
...     var = 200   # Define a new local variable using the same name, var
...
>>> func()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
    func()
  File "<stdin>", line 2, in func
    print(var)
UnboundLocalError: local variable 'var' referenced before assignment
You likely expect to be able to print the global var and be able to update var later, but again you get an UnboundLocalError. What happens here is that when you run the body of func(), Python decides that var is a local variable because it’s assigned within the function scope. This isn’t a bug, but a design choice. Python assumes that names assigned in the body of a function are local to that function.

Note: Global names can be updated or modified from any place in your global Python scope. Beyond that, the global statement can be used to modify global names from almost any place in your code, as you’ll see in The global Statement.

Modifying global names is generally considered bad programming practice because it can lead to code that is:

Difficult to debug: Almost any statement in the program can change the value of a global name.
Hard to understand: You need to be aware of all the statements that access and modify global names.
Impossible to reuse: The code is dependent on global names that are specific to a concrete program.
Good programming practice recommends using local names rather than global names. Here are some tips:

Write self-contained functions that rely on local names rather than global ones.
Try to use unique objects names, no matter what scope you’re in.
Avoid global name modifications throughout your programs.
Avoid cross-module name modifications.
Use global names as constants that don’t change during your program’s execution.
Up to this point, you’ve covered three Python scopes. Check out the following example for a summary on where they’re located in your code and how Python looks up names through them:

>>> # This area is the global or module scope
>>> number = 100
>>> def outer_func():
...     # This block is the local scope of outer_func()
...     # It's also the enclosing scope of inner_func()
...     def inner_func():
...         # This block is the local scope of inner_func()
...         print(number)
...
...     inner_func()
...
>>> outer_func()
100
When you call outer_func(), you get 100 printed on your screen. But how does Python look up the name number in this case? Following the LEGB rule, you’ll look up number in the following places:

Inside inner_func(): This is the local scope, but number doesn’t exist there.
Inside outer_func(): This is the enclosing scope, but number isn’t defined there either.
In the module scope: This is the global scope, and you find number there, so you can print number to the screen.
If number isn’t defined inside the global scope, then Python continues the search by looking at the built-in scope. This is the last component of the LEGB rule, as you’ll see in the next section.

builtins: The Built-In Scope
The built-in scope is a special Python scope that’s implemented as a standard library module named builtins in Python 3.x. All of Python’s built-in objects live in this module. They’re automatically loaded to the built-in scope when you run the Python interpreter. Python searches builtins last in its LEGB lookup, so you get all the names it defines for free. This means that you can use them without importing any module.

Notice that the names in builtins are always loaded into your global Python scope with the special name __builtins__, as you can see in the following code:

>>> dir()
['__annotations__', '__builtins__',..., '__package__', '__spec__']
>>> dir(__builtins__)
['ArithmeticError', 'AssertionError',..., 'tuple', 'type', 'vars', 'zip']
In the output of the first call to dir(), you can see that __builtins__ is always present in the global Python scope. If you inspect __builtins__ itself using dir(), then you’ll get the whole list of Python built-in names.

The built-in scope brings more than 150 names to your current global Python scope. For example, in Python 3.8 you can get to know the exact number of names as follows:

>>> len(dir(__builtins__))
152
With the call to len(), you get the number of items in the list returned by dir(). This returns 152 names that include exceptions, functions, types, special attributes, and other Python built-in objects.

Even though you can access all of these Python built-in objects for free (without importing anything), you can also explicitly import builtins and access the names using the dot notation. Here’s how this works:

>>> import builtins  # Import builtins as a regular module
>>> dir(builtins)
['ArithmeticError', 'AssertionError',..., 'tuple', 'type', 'vars', 'zip']
>>> builtins.sum([1, 2, 3, 4, 5])
15
>>> builtins.max([1, 5, 8, 7, 3])
8
>>> builtins.sorted([1, 5, 8, 7, 3])
[1, 3, 5, 7, 8]
>>> builtins.pow(10, 2)
100
You can import builtins as you would any other Python module. From this point on, you can access all the names in builtins by using the dotted attribute lookup or fully-qualified names. This can be quite useful if you want to make sure that you won’t have a name collision if any of your global names override any built-in name.

You can override or redefine any built-in name in your global scope. If you do so, then keep in mind that this will affect all your code. Take a look at the following example:

>>> abs(-15)  # Standard use of a built-in function
15
>>> abs = 20  # Redefine a built-in name in the global scope
>>> abs(-15)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'int' object is not callable
If you override or re-assign abs, then the original built-in abs() is affected all over your code. Now, suppose that you need to call the original abs() and you forget that you re-assigned the name. In this case, when you call abs() again, you’d get a TypeError because abs now holds a reference to an integer, which is not callable.

Note: Accidentally or inadvertently overriding or redefining built-in names in your global scope can be a source of dangerous and hard-to-find bugs. It’s better to try and avoid this kind of practice.

If you’re experimenting with some code and you accidentally re-assign a built-in name at the interactive prompt, then you can either restart your session or run del name to remove the redefinition from your global Python scope. This way, you’re restoring the original name in the built-in scope. If you revisit the example of abs(), then you can do something like this:

>>> del abs  # Remove the redefined abs from your global scope
>>> abs(-15)  # Restore the original abs()
15
When you delete the custom abs name, you’re removing the name from your global scope. This allows you to access the original abs() in the built-in scope again.

To work around this kind of situation, you can explicitly import builtins and then use fully-qualified names, like in the following code fragment:

>>> import builtins
>>> builtins.abs(-15)
15
Once you explicitly import builtins, you have the module name available in your global Python scope. From this point on, you can use fully-qualified names to unambiguously get the names you need from builtins, just like you did with builtins.abs() in the above example.

As a quick summary, some of the implications of Python scope are shown in the following table:

Action	Global Code	Local Code	Nested Function Code
Access or reference names that live in the global scope	Yes	Yes	Yes
Modify or update names that live in the global scope	Yes	No (unless declared global)	No (unless declared global)
Access or reference names that live in a local scope	No	Yes (its own local scope), No (other local scope)	Yes (its own local scope), No (other local scope)
Override names in the built-in scope	Yes	Yes (during function execution)	Yes (during function execution)
Access or reference names that live in their enclosing scope	N/A	N/A	Yes
Modify or update names that live in their enclosing scope	N/A	N/A	No (unless declared nonlocal)
Additionally, code in different scopes can use the same name for different objects. This way, you can use a local variable named spam and also a global variable with the same name, spam. However, this is considered bad programming practice.

Modifying the Behavior of a Python Scope
So far, you’ve learned how a Python scope works and how they restrict the visibility of variables, functions, classes, and other Python objects to certain portions of your code. You now know that you can access or reference global names from any place in your code, but they can be modified or updated from within the global Python scope.

You also know that you can access local names only from inside the local Python scope they were created in or from inside a nested function, but you can’t access them from the global Python scope or from other local scopes. Additionally, you’ve learned that nonlocal names can be accessed from inside nested functions, but they can’t be modified or updated from there.

Even though Python scopes follow these general rules by default, there are ways to modify this standard behavior. Python provides two keywords that allow you to modify the content of global and nonlocal names. These two keywords are:

global
nonlocal
In the next two sections, you’ll cover how to use these Python keywords to modify the standard behavior of Python scopes.

The global Statement
You already know that when you try to assign a value to a global name inside a function, you create a new local name in the function scope. To modify this behavior, you can use a global statement. With this statement, you can define a list of names that are going to be treated as global names.

The statement consists of the global keyword followed by one or more names separated by commas. You can also use multiple global statements with a name (or a list of names). All the names that you list in a global statement will be mapped to the global or module scope in which you define them.

Here’s an example where you try to update a global variable from within a function:

>>> counter = 0  # A global name
>>> def update_counter():
...     counter = counter + 1  # Fail trying to update counter
...
>>> update_counter()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 2, in update_counter
UnboundLocalError: local variable 'counter' referenced before assignment
When you try to assign counter inside update_counter(), Python assumes that counter is local to update_counter() and raises an UnboundLocalError because you’re trying to access a name that isn’t defined yet.

If you want this code to work the way you expect here, then you can use a global statement as follows:

>>> counter = 0  # A global name
>>> def update_counter():
...     global counter  # Declare counter as global
...     counter = counter + 1  # Successfully update the counter
...
>>> update_counter()
>>> counter
1
>>> update_counter()
>>> counter
2
>>> update_counter()
>>> counter
3
In this new version of update_counter(), you add the statement global counter to the body of the function right before you try to change counter. With this tiny change, you’re mapping the name counter in the function scope to the same name in the global or module scope. From this point on, you can freely modify counter inside update_counter(). All the changes will reflect in the global variable.

With the statement global counter, you’re telling Python to look in the global scope for the name counter. This way, the expression counter = counter + 1 doesn’t create a new name in the function scope, but updates it in the global scope.

Note: The use of global is considered bad practice in general. If you find yourself using global to fix problems like the one above, then stop and think if there is a better way to write your code.

For example, you can try to write a self-contained function that relies on local names rather than on global names as follows:

>>> global_counter = 0  # A global name
>>> def update_counter(counter):
...     return counter + 1  # Rely on a local name
...
>>> global_counter = update_counter(global_counter)
>>> global_counter
1
>>> global_counter = update_counter(global_counter)
>>> global_counter
2
>>> global_counter = update_counter(global_counter)
>>> global_counter
3
This implementation of update_counter() defines counter as a parameter and returns its value augmented by 1 unit every time the function is called. This way, the result of update_counter() depends on the counter you use as an input and not on the changes that other functions (or pieces of code) can perform on the global variable, global_counter.

You can also use a global statement to create lazy global names by declaring them inside a function. Take a look at the following code:

>>> def create_lazy_name():
...     global lazy  # Create a global name, lazy
...     lazy = 100
...     return lazy
...
>>> create_lazy_name()
100
>>> lazy  # The name is now available in the global scope
100
>>> dir()
['__annotations__', '__builtins__',..., 'create_lazy_name', 'lazy']
When you call create_lazy_name(), you’re also creating a global variable called lazy. Notice that after calling the function, the name lazy is available in the global Python scope. If you inspect the global namespace using dir(), then you’ll see that lazy appears last in the list.

Note: Even though you can use a global statement to create lazy global names, this can be a dangerous practice that can lead to buggy code. So, it’s best to avoid things like this in your code.

For example, suppose you’re trying to get access to one of those lazy names and, for some reason, your code hasn’t called the function that creates that name yet. In this case, you’ll get a NameError and your program will crash.

Finally, it’s worth noting that you can use global from inside any function or nested function and the names listed will always be mapped to names in the global Python scope.

Also notice that, even though using a global statement at the top level of a module is legal, it doesn’t make much sense because any name assigned in the global scope is already a global name by definition. Take a look at the following code:

>>> name = 100
>>> dir()
['__annotations__', '__builtins__',..., '__spec__', 'name']
>>> global name
>>> dir()
['__annotations__', '__builtins__',..., '__spec__', 'name']
The use of a global statement like global name doesn’t change anything in your current global scope, as you can see in the output of dir(). The variable name is a global variable whether you use global or not.