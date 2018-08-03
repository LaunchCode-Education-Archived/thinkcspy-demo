..  Copyright (C)  Brad Miller, David Ranum, Jeffrey Elkner, Peter Wentworth, Allen B. Downey, Chris
    Meyers, and Dario Mitchell. Permission is granted to copy, distribute
    and/or modify this document under the terms of the GNU Free Documentation
    License, Version 1.3 or any later version published by the Free Software
    Foundation; with Invariant Sections being Forward, Prefaces, and
    Contributor List, no Front-Cover Texts, and no Back-Cover Texts. A copy of
    the license is included in the section entitled "GNU Free Documentation
    License".

5.2 Functions That Return Values
================================

Most functions require arguments --- values that control how the function does its job. For example, if you want to find the absolute value of a number, you have to indicate what the number is. Python has a built-in function for computing the absolute value:

    .. raw:: html

        <iframe height="400px" width="100%" src="https://repl.it/@launchcode/Demo-Ch-52a?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

In this example, the arguments to the ``abs`` function are 5 and -5.

Some functions take more than one argument. For example the math module contains a function called ``pow`` which takes two arguments, the base and the exponent.

    .. raw:: html

        <iframe height="400px" width="100%" src="https://repl.it/@launchcode/Demo-Ch-52b?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

.. note::

     Of course, we have already seen that raising a base to an exponent can be done with the ** operator.

Another built-in function that takes more than one argument is ``max``.

    .. raw:: html

        <iframe height="400px" width="100%" src="https://repl.it/@launchcode/Demo-Ch-52c?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

``max`` can be sent any number of arguments, separated by commas, and will return the maximum value sent. The arguments can be either simple values or expressions. In the last example, 503 is returned, since it is larger than 33, 125, and 1. Note that ``max`` also works on lists of values.

Furthermore, functions like ``range``, ``int``, ``abs`` all return values that can be used to build more complex expressions.

So an important difference between these functions and one like ``draw_square`` is that ``draw_square`` was not executed because we wanted it to return a value --- on the contrary, we called ``draw_square`` because we wanted it to execute a sequence of steps that caused the turtle to draw a specific shape.

Functions that return values are sometimes called **fruitful functions**. In many other languages, a chunk that *doesn't* return a value is called a **procedure**, but we will stick here with the Python way of simply calling it a function, or if we want to stress its lack of a return value, a *non-fruitful* function.

As you've seen, fruitful functions still allow the user to provide information (arguments). They just additionally return data from the function, which is their difference from non-fruitful functions.

.. image:: _static/images/blackboxfun.png


How do we write our own fruitful function? Let's start by creating a very simple mathematical function that we will call ``square``.  The ``square`` function will take one number as a parameter and return the result of squaring that number. Here is the black-box diagram with the Python code following.

.. image:: _static/images/squarefun.png
.. 

    .. raw:: html

        <iframe height="400px" width="100%" src="https://repl.it/@launchcode/Demo-Ch-52d?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

The **return** statement is followed by an expression which is evaluated. Its result is returned to the caller as the "fruit" of calling this function. Because the return statement can contain any Python expression we could have avoided creating the **temporary variable** ``y`` and simply used ``return x * x``. Try modifying the square function above to see that this works just the same.

On the other hand, sometimes using **temporary variables** like ``y`` in the program above makes debugging easier. These temporary variables are referred to as **local variables**.

Notice something important here. The name of the variable we pass as an argument, ``num``, has nothing to do with the name of the formal parameter, ``x``.  It is as if ``x = num`` is executed when ``square`` is called. It doesn't matter what the value was named in the caller. Inside the ``square`` function, it's name is ``x``.  You can see this very clearly in codelens, where the global variables and the local variables for the ``square`` function are in separate boxes.

As you step through the example in codelens notice that the **return** statement not only causes the function to return a value, but it also returns the flow of control back to the place in the program where the function call was made.

    .. raw:: html

        <iframe width="800" height="500" frameborder="0" src="http://pythontutor.com/iframe-embed.html#code=def%20square%28x%29%3A%0A%20%20%20%20y%20%3D%20x%20*%20x%0A%20%20%20%20return%20y%0A%20%20%20%20%0Anum%20%3D%2010%0Aresult%20%3D%20square%28num%29%0Aprint%28%22The%20result%20of%20%22,%20num,%20%22%20squared%20is%20%22,%20result%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>


Another important thing to notice as you step through this codelens is the movement of the red and green arrows. Codelens uses these arrows to show you where it is currently executing. Recall that the red arrow always points to the next line of code that will be executed. The light green arrow points to the line that was just executed in the last step.

When you first start running this codelens you will notice that there is only a red arrow and it points to line 1. This is because line 1 is the next line to be executed and since it is the first line, there is no previously executed line of code.

When you click on the forward button, notice that the red arrow moves to line 5, skipping lines 2 and 3 of the function (and the light green arrow has now appeared on line 1).  Why is this? The answer is that function definition is not the same as function execution. Lines 2 and 3 will not be executed until the function is called on line 6. Line 1 defines the function and the name ``square`` is added to the global variables, but that is all the ``def`` does at that point. The body of the function will be executed later. Continue to click the forward button to see how the flow of control moves from the call, back up to the body of the function, and then finally back to line 7, after the function has returned its value and the value has been assigned to ``result``.

Finally, there is one more aspect of function return values that should be noted. All Python functions return the value ``None`` unless there is an explicit return statement with a value other than ``None``. Consider the following common mistake made by beginning Python programmers. As you step through this example, pay very close attention to the return value in the local variables listing. Then look at what is printed when the function returns.

    .. raw:: html

        <iframe width="800" height="500" frameborder="0" src="http://pythontutor.com/iframe-embed.html#code=def%20square%28x%29%3A%0A%20%20%20%20y%20%3D%20x%20*%20x%0A%20%20%20%20print%28y%29%20%20%20%23%20Bad!%20should%20use%20return%20instead!%0A%20%20%20%20%0Anum%20%3D%2010%0Aresult%20%3D%20square%28num%29%0Aprint%28%22The%20result%20of%20%22,%20num,%20%22%20squared%20is%20%22,%20result%29%0A&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

The problem with this function is that even though it prints the value of the square, that value will not be returned to the place where the call was done. Since line 6 uses the return value as the right hand side of an assignment statement, the evaluation of the function will be ``None``.  In this case, ``result`` will refer to that value after the assignment statement and therefore the result printed in line 7 is incorrect. Typically, functions will return values that can be printed or processed in some other way by the caller.


**Check your understanding**

Check Canvas for review quiz
