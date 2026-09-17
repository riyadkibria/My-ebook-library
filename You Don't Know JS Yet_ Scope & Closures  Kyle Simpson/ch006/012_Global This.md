# ch006

## Global This


Reviewing the JS environments we’ve looked at so far, a program may or may not:

Declare a global variable in the top-level scope with var or function declarations—or let, const, and class.

Also add global variables declarations as properties of the global scope object if var or function are used for the declaration.

Refer to the global scope object (for adding or retrieving global variables, as properties) with window, self, or global.

I think it’s fair to say that global scope access and behavior is more complicated than most developers assume, as the preceding sections have illustrated. But the complexity is never more obvious than in trying to nail down a universally applicable reference to the global scope object.

Yet another “trick” for obtaining a reference to the global scope object looks like:

So, we have window, self, global, and this ugly new Function(..) trick. That’s a lot of different ways to try to get at this global object. Each has its pros and cons.

Why not introduce yet another!?!?

As of ES2020, JS has finally defined a standardized reference to the global scope object, called globalThis. So, subject to the recency of the JS engines your code runs in, you can use globalThis in place of any of those other approaches.

We could even attempt to define a cross-environment polyfill that’s safer across pre-globalThis JS environments, such as:

Phew! That’s certainly not ideal, but it works if you find yourself needing a reliable global scope reference.

(The proposed name globalThis was fairly controversial while the feature was being added to JS. Specifically, I and many others felt the “this” reference in its name was misleading, since the reason you reference this object is to access to the global scope, never to access some sort of global/default this binding. There were many other names considered, but for a variety of reasons ruled out. Unfortunately, the name chosen ended up as a last resort. If you plan to interact with the global scope object in your programs, to reduce confusion, I strongly recommend choosing a better name, such as (the laughably long but accurate!) theGlobalScopeObject used here.)
