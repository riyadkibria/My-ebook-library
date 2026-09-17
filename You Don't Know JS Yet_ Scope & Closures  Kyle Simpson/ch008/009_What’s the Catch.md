# ch008

## What’s the Catch?


So far we’ve asserted that var and parameters are function-scoped, and let/const signal block-scoped declarations. There’s one little exception to call out: the catch clause.

Since the introduction of try..catch back in ES3 (in 1999), the catch clause has used an additional (little-known) block-scoping declaration capability:

The err variable declared by the catch clause is block-scoped to that block. This catch clause block can hold other block-scoped declarations via let. But a var declaration inside this block still attaches to the outer function/global scope.

ES2019 (recently, at the time of writing) changed catch clauses so their declaration is optional; if the declaration is omitted, the catch block is no longer (by default) a scope; it’s still a block, though!

So if you need to react to the condition that an exception occurred (so you can gracefully recover), but you don’t care about the error value itself, you can omit the catch declaration:

This is a small but delightful simplification of syntax for a fairly common use case, and may also be slightly more performant in removing an unnecessary scope!
