# ch011

## Function Hoisting


To review, this program works because of function hoisting:

The function declaration is hoisted during compilation, which means that getStudents is an identifier declared for the entire scope. Additionally, the getStudents identifier is auto-initialized with the function reference, again at the beginning of the scope.

Why is this useful? The reason I prefer to take advantage of function hoisting is that it puts the executable code in any scope at the top, and any further declarations (functions) below. This means it’s easier to find the code that will run in any given area, rather than having to scroll and scroll, hoping to find a trailing } marking the end of a scope/function somewhere.

I take advantage of this inverse positioning in all levels of scope:

When I first open a file like that, the very first line is executable code that kicks off its behavior. That’s very easy to spot! Then, if I ever need to go find and inspect getStudents(), I like that its first line is also executable code. Only if I need to see the details of doSomething() do I go and find its definition down below.

In other words, I think function hoisting makes code more readable through a flowing, progressive reading order, from top to bottom.
