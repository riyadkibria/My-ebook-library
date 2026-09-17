# ch010

## Modules (Stateful Access Control)


To embody the full spirit of the module pattern, we not only need grouping and state, but also access control through visibility (private vs. public).

Let’s turn Student from the previous section into a module. We’ll start with a form I call the “classic module,” which was originally referred to as the “revealing module” when it first emerged in the early 2000s. Consider:

Student is now an instance of a module. It features a public API with a single method: getName(..). This method is able to access the private hidden records data.

How does the classic module format work?

Notice that the instance of the module is created by the defineStudent() IIFE being executed. This IIFE returns an object (named publicAPI) that has a property on it referencing the inner getName(..) function.

Naming the object publicAPI is stylistic preference on my part. The object can be named whatever you like (JS doesn’t care), or you can just return an object directly without assigning it to any internal named variable. More on this choice in Appendix A.

From the outside, Student.getName(..) invokes this exposed inner function, which maintains access to the inner records variable via closure.

You don’t have to return an object with a function as one of its properties. You could just return a function directly, in place of the object. That still satisfies all the core bits of a classic module.

By virtue of how lexical scope works, defining variables and functions inside your outer module definition function makes everything by default private. Only properties added to the public API object returned from the function will be exported for external public use.

The use of an IIFE implies that our program only ever needs a single central instance of the module, commonly referred to as a “singleton.” Indeed, this specific example is simple enough that there’s no obvious reason we’d need anything more than just one instance of the Student module.
