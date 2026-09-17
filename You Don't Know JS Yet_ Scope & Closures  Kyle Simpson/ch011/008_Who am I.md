# ch011

## Who am I?


Without a lexical name identifier, the function has no internal way to refer to itself. Self-reference is important for things like recursion and event handling:

Leaving off the lexical name from your callback makes it harder to reliably self-reference the function. You could declare a variable in an enclosing scope that references the function, but this variable is controlled by that enclosing scope—it could be re-assigned, etc.—so it’s not as reliable as the function having its own internal self-reference.
