# ch003

## Early Errors


The "Howdy" message is not printed, despite being a well-formed statement.

Instead, just like the snippet in the previous section, the SyntaxError here is thrown before the program is executed. In this case, it’s because strict-mode (opted in for only the saySomething(..) function here) forbids, among many other things, functions to have duplicate parameter names; this has always been allowed in non-strict-mode.

The error thrown is not a syntax error in the sense of being a malformed string of tokens (like ."Hi" prior), but in strict-mode is nonetheless required by the specification to be thrown as an “early error” before any execution begins.

But how does the JS engine know that the greeting parameter has been duplicated? How does it know that the saySomething(..) function is even in strict-mode while processing the parameter list (the "use strict" pragma appears only later, in the function body)?

Again, the only reasonable explanation is that the code must first be fully parsed before any execution occurs.
