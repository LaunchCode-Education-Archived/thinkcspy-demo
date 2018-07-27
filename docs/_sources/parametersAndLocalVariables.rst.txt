..  Copyright (C)  Brad Miller, David Ranum, Jeffrey Elkner, Peter Wentworth, Allen B. Downey, Chris
    Meyers, and Dario Mitchell. Permission is granted to copy, distribute
    and/or modify this document under the terms of the GNU Free Documentation
    License, Version 1.3 or any later version published by the Free Software
    Foundation; with Invariant Sections being Forward, Prefaces, and
    Contributor List, no Front-Cover Texts, and no Back-Cover Texts. A copy of
    the license is included in the section entitled "GNU Free Documentation
    License".

5.3 Parameters and Local Variables
==================================

An assignment statement in a function creates a **local variable** for the variable on the left hand side of the assignment operator. It is called local because this variable only exists inside the function and you cannot use it outside of it. For example, consider again the ``square`` function:

    .. raw:: html

        <iframe width="800" height="500" frameborder="0" src="http://pythontutor.com/iframe-embed.html#code=def%20square%28x%29%3A%0A%20%20%20%20y%20%3D%20x%20*%20x%0A%20%20%20%20return%20y%0A%0Az%20%3D%20square%2810%29%0Aprint%28y%29%0A&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

If you press the "last >>" button you will see an error message. When we try to use ``y`` on line 6 (outside the function) Python looks for a global variable named ``y`` but does not find one. This results in the error: ``NameError: 'y' is not defined.``

The variable ``y`` only exists while the function is being executed --- we call this its **lifetime**. When the execution of the function terminates (returns), the local variables are destroyed. Codelens helps you  visualize this because the local variables disappear after the function returns. Go back and step through the statements paying particular attention to the variables that are created when the function is called. Note when they are subsequently destroyed as the function returns.

Formal parameters are also local and act like local variables. For example, the lifetime of ``x`` begins when ``square`` is called, and its lifetime ends when the function completes its execution.

So it is not possible for a function to set some local variable to a value, complete its execution, and then when it is called again next time, recover the local variable. Each call of the function creates new local variables, and their lifetimes expire when the function returns to the caller.

On the other hand, it is legal for a function to access a global variable. However, this is considered **bad form** by nearly all programmers and should be avoided. Look at the following variation on the ``square`` function.

    .. raw:: html

        <iframe height="400px" width="100%" src="https://repl.it/@launchcode/Demo-Ch-53b?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Although the ``bad_square`` function works, it is poorly written. We have done it here to illustrate an important rule about how variables are looked up in Python. First, Python looks at the variables that are defined as local variables in the function. We call this the **local scope**.  If the variable name is not found in the local scope, then Python looks at the global variables, or **global scope**.  This is exactly the case illustrated in the code above. While ``power`` is not found locally in ``bad_square``, it does exist globally and therefore can be used in the function. But the appropriate way to write this function would be to pass ``power`` as an argument to the ``square`` function. For practice, you should rewrite the ``bad_square`` example to have a second parameter called ``power``.

There is another important aspect of local versus global variables: *assignment statements in the local function cannot change variables defined outside the function*. Consider the following codelens example:

    .. raw:: html

        <iframe width="800" height="500" frameborder="0" src="http://pythontutor.com/iframe-embed.html#code=def%20power_of%28x,%20p%29%3A%0A%20%20%20%20power%20%3D%20p%20%20%20%23%20Another%20dumb%20mistake%0A%20%20%20%20y%20%3D%20x%20**%20power%0A%20%20%20%20return%20y%0A%0Apower%20%3D%203%0Aresult%20%3D%20power_of%2810,%202%29%0Aprint%28result%29%0A&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Now step through the code. What do you notice about the values of variable ``power`` in the local scope compared to the variable ``power`` in the global scope?

The value of ``power`` in the local scope was different than the global scope. That is because in this example ``power`` was used on the left hand side of the assignment statement ``power = p``.  When a variable name is used on the left hand side of an assignment statement Python creates a local variable. When a local variable has the same name as a global variable we say that the local shadows the global. A **shadow** means that the global variable cannot be accessed by Python because the local variable will be found first. This is another good reason not to use global variables. As you can see, it makes your code confusing and difficult to understand.

To cement all of these ideas even further let's look at one final example. Inside the ``square`` function we are going to make an assignment to the parameter ``x``  There's no good reason to do this other than to emphasize the fact that the parameter ``x`` is a local variable. If you step through the example in codelens you will see that although ``x`` is 0 in the local variable for ``square``, the ``x`` in the global scope remains 2. This is confusing to many beginning programmers who think that an assignment to a formal parameter will cause a change to the value of the variable that was used as the actual parameter (the argument), especially when the two share the same name. But this example demonstrates that Python clearly does not operate that way.

    .. raw:: html

        <iframe width="800" height="500" frameborder="0" src="http://pythontutor.com/iframe-embed.html#code=def%20square%28x%29%3A%0A%20%20%20%20y%20%3D%20x%20*%20x%0A%20%20%20%20x%20%3D%200%20%20%20%20%20%20%20%23%20assign%20a%20new%20value%20to%20the%20parameter%20x%0A%20%20%20%20return%20y%0A%0Ax%20%3D%202%0Az%20%3D%20square%28x%29%0Aprint%28z%29%0A&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=9&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

**Check your understanding**

See Canvas for review quizzes

