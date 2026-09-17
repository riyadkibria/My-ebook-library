# ch011

## Missing Names?


Yes, these inferred names might show up in stack traces, which is definitely better than “anonymous” showing up. But…

Oops. Anonymous function expressions passed as callbacks are incapable of receiving an inferred name, so cb.name holds just the empty string "". The vast majority of all function expressions, especially anonymous ones, are used as callback arguments; none of these get a name. So relying on name inference is incomplete, at best.

And it’s not just callbacks that fall short with inference:

Any assignment of a function expression that’s not a simple assignment will also fail name inferencing. So, in other words, unless you’re careful and intentional about it, essentially almost all anonymous function expressions in your program will in fact have no name at all.

Name inference is just… not enough.

And even if a function expression does get an inferred name, that still doesn’t count as being a full named function.
