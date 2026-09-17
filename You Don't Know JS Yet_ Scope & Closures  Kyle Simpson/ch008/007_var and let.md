# ch008

## var and let


Next, let’s talk about the declaration var buckets. That variable is used across the entire function (except the final return statement). Any variable that is needed across all (or even most) of a function should be declared so that such usage is obvious.

So why did we use var instead of let to declare the buckets variable? There’s both semantic and technical reasons to choose var here.

Stylistically, var has always, from the earliest days of JS, signaled “variable that belongs to a whole function.” As we asserted in “Lexical Scope” (Chapter 1), var attaches to the nearest enclosing function scope, no matter where it appears. That’s true even if var appears inside a block:

Even though var is inside a block, its declaration is function-scoped (to diff(..)), not block-scoped.

While you can declare var inside a block (and still have it be function-scoped), I would recommend against this approach except in a few specific cases (discussed in Appendix A). Otherwise, var should be reserved for use in the top-level scope of a function.

Why not just use let in that same location? Because var is visually distinct from let and therefore signals clearly, “this variable is function-scoped.” Using let in the top-level scope, especially if not in the first few lines of a function, and when all the other declarations in blocks use let, does not visually draw attention to the difference with the function-scoped declaration.

In other words, I feel var better communicates function-scoped than let does, and let both communicates (and achieves!) block-scoping where var is insufficient. As long as your programs are going to need both function-scoped and block-scoped variables, the most sensible and readable approach is to use both var and let together, each for their own best purpose.

There are other semantic and operational reasons to choose var or let in different scenarios. We’ll explore the case for var and let in more detail in Appendix A.
