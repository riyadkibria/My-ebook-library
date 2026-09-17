# ch005

## Global Unshadowing Trick


Please beware: leveraging the technique I’m about to describe is not very good practice, as it’s limited in utility, confusing for readers of your code, and likely to invite bugs to your program. I’m covering it only because you may run across this behavior in existing programs, and understanding what’s happening is critical to not getting tripped up.

It is possible to access a global variable from a scope where that variable has been shadowed, but not through a typical lexical identifier reference.

In the global scope (RED(1)), var declarations and function declarations also expose themselves as properties (of the same name as the identifier) on the global object—essentially an object representation of the global scope. If you’ve written JS for a browser environment, you probably recognize the global object as window. That’s not entirely accurate, but it’s good enough for our discussion. In the next chapter, we’ll explore the global scope/object topic more.

Consider this program, specifically executed as a standalone .js file in a browser environment:

Notice the window.studentName reference? This expression is accessing the global variable studentName as a property on window (which we’re pretending for now is synonymous with the global object). That’s the only way to access a shadowed variable from inside a scope where the shadowing variable is present.

The window.studentName is a mirror of the global studentName variable, not a separate snapshot copy. Changes to one are still seen from the other, in either direction. You can think of window.studentName as a getter/setter that accesses the actual studentName variable. As a matter of fact, you can even add a variable to the global scope by creating/setting a property on the global object.

This little “trick” only works for accessing a global scope variable (not a shadowed variable from a nested scope), and even then, only one that was declared with var or function.

Other forms of global scope declarations do not create mirrored global object properties:

Variables (no matter how they’re declared!) that exist in any other scope than the global scope are completely inaccessible from a scope where they’ve been shadowed:

The global RED(1) special is shadowed by the BLUE(2) special (parameter), and the BLUE(2) special is itself shadowed by the GREEN(3) special inside keepLooking(). We can still access the RED(1) special using the indirect reference window.special. But there’s no way for keepLooking() to access the BLUE(2) special that holds the number 112358132134.
