# ch005

## Illegal Shadowing


Not all combinations of declaration shadowing are allowed. let can shadow var, but var cannot shadow let:

Notice in the another() function, the inner var special declaration is attempting to declare a function-wide special, which in and of itself is fine (as shown by the something() function).

The syntax error description in this case indicates that special has already been defined, but that error message is a little misleading—again, no such error happens in something(), as shadowing is generally allowed just fine.

The real reason it’s raised as a SyntaxError is because the var is basically trying to “cross the boundary” of (or hop over) the let declaration of the same name, which is not allowed.

That boundary-crossing prohibition effectively stops at each function boundary, so this variant raises no exception:

Summary: let (in an inner scope) can always shadow an outer scope’s var. var (in an inner scope) can only shadow an outer scope’s let if there is a function boundary in between.
