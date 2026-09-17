# ch007

## Re-declaration?


What do you think happens when a variable is declared more than once in the same scope? Consider:

What do you expect to be printed for that second message? Many believe the second var studentName has re-declared the variable (and thus “reset” it), so they expect undefined to be printed.

But is there such a thing as a variable being “re-declared” in the same scope? No.

If you consider this program from the perspective of the hoisting metaphor, the code would be re-arranged like this for execution purposes:

Since hoisting is actually about registering a variable at the beginning of a scope, there’s nothing to be done in the middle of the scope where the original program actually had the second var studentName statement. It’s just a no-op(eration), a pointless statement.

It’s also important to point out that var studentName; doesn’t mean var studentName = undefined;, as most assume. Let’s prove they’re different by considering this variation of the program:

See how the explicit = undefined initialization produces a different outcome than assuming it happens implicitly when omitted? In the next section, we’ll revisit this topic of initialization of variables from their declarations.

A repeated var declaration of the same identifier name in a scope is effectively a do-nothing operation. Here’s another illustration, this time across a function of the same name:

The first greeting declaration registers the identifier to the scope, and because it’s a var the auto-initialization will be undefined. The function declaration doesn’t need to re-register the identifier, but because of function hoisting it overrides the auto-initialization to use the function reference. The second var greeting by itself doesn’t do anything since greeting is already an identifier and function hoisting already took precedence for the auto-initialization.

Actually assigning "Hello!" to greeting changes its value from the initial function greeting() to the string; var itself doesn’t have any effect.

What about repeating a declaration within a scope using let or const?

This program will not execute, but instead immediately throw a SyntaxError. Depending on your JS environment, the error message will indicate something like: “studentName has already been declared.” In other words, this is a case where attempted “re-declaration” is explicitly not allowed!

It’s not just that two declarations involving let will throw this error. If either declaration uses let, the other can be either let or var, and the error will still occur, as illustrated with these two variations:

In both cases, a SyntaxError is thrown on the second declaration. In other words, the only way to “re-declare” a variable is to use var for all (two or more) of its declarations.

But why disallow it? The reason for the error is not technical per se, as var “re-declaration” has always been allowed; clearly, the same allowance could have been made for let.

It’s really more of a “social engineering” issue. “Re-declaration” of variables is seen by some, including many on the TC39 body, as a bad habit that can lead to program bugs. So when ES6 introduced let, they decided to prevent “re-declaration” with an error.

When Compiler asks Scope Manager about a declaration, if that identifier has already been declared, and if either/both declarations were made with let, an error is thrown. The intended signal to the developer is “Stop relying on sloppy re-declaration!”
