# ch011

## Variable Hoisting


What about variable hoisting?

Even though let and const hoist, you cannot use those variables in their TDZ (see Chapter 5). So, the following discussion only applies to var declarations. Before I continue, I’ll admit: in almost all cases, I completely agree that variable hoisting is a bad idea:

While that kind of inverted ordering was helpful for function hoisting, here I think it usually makes code harder to reason about.

But there’s one exception that I’ve found, somewhat rarely, in my own coding. It has to do with where I place my var declarations inside a CommonJS module definition.

Here’s how I typically structure my module definitions in Node:

Notice how the cache and otherData variables are in the “private” section of the module layout? That’s because I don’t plan to expose them publicly. So I organize the module so they’re located alongside the other hidden implementation details of the module.

But I’ve had a few rare cases where I needed the assignments of those values to happen above, before I declare the exported public API of the module. For instance:

I need the cache variable to have already been assigned a value, because that value is used in the initialization of the public API (the .bind(..) partial-application).

Should I just move the var cache = { .. } up to the top, above this public API initialization? Well, perhaps. But now it’s less obvious that var cache is a private implementation detail. Here’s the compromise I’ve (somewhat rarely) used:

See the variable hoisting? I’ve declared the cache down where it belongs, logically, but in this rare case I’ve used it earlier up above, in the area where its initialization is needed. I even left a hint at the value that’s assigned to cache in a code comment.

That’s literally the only case I’ve ever found for leveraging variable hoisting to assign a variable earlier in a scope than its declaration. But I think it’s a reasonable exception to employ with caution.
