# ch008

## Function Declarations in Blocks (FiB)


We’ve seen now that declarations using let or const are block-scoped, and var declarations are function-scoped. So what about function declarations that appear directly inside blocks? As a feature, this is called “FiB.”

We typically think of function declarations like they’re the equivalent of a var declaration. So are they function-scoped like var is?

No and yes. I know… that’s confusing. Let’s dig in:

What do you expect for this program to do? Three reasonable outcomes:

The ask() call might fail with a ReferenceError exception, because the ask identifier is block-scoped to the if block scope and thus isn’t available in the outer/global scope.

The ask() call might fail with a TypeError exception, because the ask identifier exists, but it’s undefined (since the if statement doesn’t run) and thus not a callable function.

The ask() call might run correctly, printing out the “Does it run?” message.

Here’s the confusing part: depending on which JS environment you try that code snippet in, you may get different results! This is one of those few crazy areas where existing legacy behavior betrays a predictable outcome.

The JS specification says that function declarations inside of blocks are block-scoped, so the answer should be (1). However, most browser-based JS engines (including v8, which comes from Chrome but is also used in Node) will behave as (2), meaning the identifier is scoped outside the if block but the function value is not automatically initialized, so it remains undefined.

Why are browser JS engines allowed to behave contrary to the specification? Because these engines already had certain behaviors around FiB before ES6 introduced block scoping, and there was concern that changing to adhere to the specification might break some existing website JS code. As such, an exception was made in Appendix B of the JS specification, which allows certain deviations for browser JS engines (only!).

One of the most common use cases for placing a function declaration in a block is to conditionally define a function one way or another (like with an if..else statement) depending on some environment state. For example:

It’s tempting to structure code this way for performance reasons, since the typeof Array.isArray check is only performed once, as opposed to defining just one isArray(..) and putting the if statement inside it—the check would then run unnecessarily on every call.

In addition to the previous snippets, several other FiB corner cases are lurking; such behaviors in various browsers and non-browser JS environments (JS engines that aren’t browser based) will likely vary. For example:

Recall that function hoisting as described in “When Can I Use a Variable?” (in Chapter 5) might suggest that the final ask() in this snippet, with “Wait, maybe…” as its message, would hoist above the call to ask(). Since it’s the last function declaration of that name, it should “win,” right? Unfortunately, no.

It’s not my intention to document all these weird corner cases, nor to try to explain why each of them behaves a certain way. That information is, in my opinion, arcane legacy trivia.

My real concern with FiB is, what advice can I give to ensure your code behaves predictably in all circumstances?

As far as I’m concerned, the only practical answer to avoiding the vagaries of FiB is to simply avoid FiB entirely. In other words, never place a function declaration directly inside any block. Always place function declarations anywhere in the top-level scope of a function (or in the global scope).

So for the earlier if..else example, my suggestion is to avoid conditionally defining functions if at all possible. Yes, it may be slightly less performant, but this is the better overall approach:

If that performance hit becomes a critical path issue for your application, I suggest you consider this approach:

It’s important to notice that here I’m placing a function expression, not a declaration, inside the if statement. That’s perfectly fine and valid, for function expressions to appear inside blocks. Our discussion about FiB is about avoiding function declarations in blocks.

Even if you test your program and it works correctly, the small benefit you may derive from using FiB style in your code is far outweighed by the potential risks in the future for confusion by other developers, or variances in how your code runs in other JS environments.

FiB is not worth it, and should be avoided.
