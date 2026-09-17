# ch004

## Global… What!?


If the variable is a target and strict-mode is not in effect, a confusing and surprising legacy behavior kicks in. The troublesome outcome is that the global scope’s Scope Manager will just create an accidental global variable to fulfill that target assignment!

Here’s how that conversation will proceed:

Engine: Hey, Scope Manager (for the function), I have a target reference for nextStudent, ever heard of it?

(Function) Scope Manager: Nope, never heard of it. Try the next outer scope.

Engine: Hey, Scope Manager (for the global scope), I have a target reference for nextStudent, ever heard of it?

(Global) Scope Manager: Nope, but since we’re in non-strict-mode, I helped you out and just created a global variable for you, here it is!

This sort of accident (almost certain to lead to bugs eventually) is a great example of the beneficial protections offered by strict-mode, and why it’s such a bad idea not to be using strict-mode. In strict-mode, the Global Scope Manager would instead have responded:

(Global) Scope Manager: Nope, never heard of it. Sorry, I’ve got to throw a ReferenceError.

Assigning to a never-declared variable is an error, so it’s right that we would receive a ReferenceError here.

Never rely on accidental global variables. Always use strict-mode, and always formally declare your variables. You’ll then get a helpful ReferenceError if you ever mistakenly try to assign to a not-declared variable.
