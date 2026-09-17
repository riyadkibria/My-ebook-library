# ch008

## Function Boundaries


Beware that using an IIFE to define a scope can have some unintended consequences, depending on the code around it. Because an IIFE is a full function, the function boundary alters the behavior of certain statements/constructs.

For example, a return statement in some piece of code would change its meaning if an IIFE is wrapped around it, because now the return would refer to the IIFE’s function. Non-arrow function IIFEs also change the binding of a this keyword—more on that in the Objects & Classes book. And statements like break and continue won’t operate across an IIFE function boundary to control an outer loop or block.

So, if the code you need to wrap a scope around has return, this, break, or continue in it, an IIFE is probably not the best approach. In that case, you might look to create the scope with a block instead of a function.
