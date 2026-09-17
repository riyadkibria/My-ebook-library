# ch004

## Nested Scope


When it comes time to execute the getStudentName() function, Engine asks for a Scope Manager instance for that function’s scope, and it will then proceed to look up the parameter (studentID) to assign the 73 argument value to, and so on.

The function scope for getStudentName(..) is nested inside the global scope. The block scope of the for-loop is similarly nested inside that function scope. Scopes can be lexically nested to any arbitrary depth as the program defines.

Each scope gets its own Scope Manager instance each time that scope is executed (one or more times). Each scope automatically has all its identifiers registered at the start of the scope being executed (this is called “variable hoisting”; see Chapter 5).

At the beginning of a scope, if any identifier came from a function declaration, that variable is automatically initialized to its associated function reference. And if any identifier came from a var declaration (as opposed to let/const), that variable is automatically initialized to undefined so that it can be used; otherwise, the variable remains uninitialized (aka, in its “TDZ,” see Chapter 5) and cannot be used until its full declaration-and-initialization are executed.

In the for (let student of students) { statement, students is a source reference that must be looked up. But how will that lookup be handled, since the scope of the function will not find such an identifier?

To explain, let’s imagine that bit of conversation playing out like this:

Engine: Hey, Scope Manager (for the function), I have a source reference for students, ever heard of it?

(Function) Scope Manager: Nope, never heard of it. Try the next outer scope.

Engine: Hey, Scope Manager (for the global scope), I have a source reference for students, ever heard of it?

(Global) Scope Manager: Yep, it was formally declared, here it is.

One of the key aspects of lexical scope is that any time an identifier reference cannot be found in the current scope, the next outer scope in the nesting is consulted; that process is repeated until an answer is found or there are no more scopes to consult.
