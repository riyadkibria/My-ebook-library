# ch010

## Module Factory (Multiple Instances)


But if we did want to define a module that supported multiple instances in our program, we can slightly tweak the code:

Rather than specifying defineStudent() as an IIFE, we just define it as a normal standalone function, which is commonly referred to in this context as a “module factory” function.

We then call the module factory, producing an instance of the module that we label fullTime. This module instance implies a new instance of the inner scope, and thus a new closure that getName(..) holds over records. fullTime.getName(..) now invokes the method on that specific instance.
