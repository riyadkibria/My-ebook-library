# ch007

## When Can I Use a Variable?


At what point does a variable become available to use within its scope? There may seem to be an obvious answer: after the variable has been declared/created. Right? Not quite.

This code works fine. You may have seen or even written code like it before. But did you ever wonder how or why it works? Specifically, why can you access the identifier greeting from line 1 (to retrieve and execute a function reference), even though the greeting() function declaration doesn’t occur until line 4?

Recall Chapter 1 points out that all identifiers are registered to their respective scopes during compile time. Moreover, every identifier is created at the beginning of the scope it belongs to, every time that scope is entered.

The term most commonly used for a variable being visible from the beginning of its enclosing scope, even though its declaration may appear further down in the scope, is called hoisting.

But hoisting alone doesn’t fully answer the question. We can see an identifier called greeting from the beginning of the scope, but why can we call the greeting() function before it’s been declared?

In other words, how does the variable greeting have any value (the function reference) assigned to it, from the moment the scope starts running? The answer is a special characteristic of formal function declarations, called function hoisting. When a function declaration’s name identifier is registered at the top of its scope, it’s additionally auto-initialized to that function’s reference. That’s why the function can be called throughout the entire scope!

One key detail is that both function hoisting and var-flavored variable hoisting attach their name identifiers to the nearest enclosing function scope (or, if none, the global scope), not a block scope.
