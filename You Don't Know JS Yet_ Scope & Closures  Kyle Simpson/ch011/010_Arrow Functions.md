# ch011

## Arrow Functions


Arrow functions are always anonymous, even if (rarely) they’re used in a way that gives them an inferred name. I just spent several pages explaining why anonymous functions are a bad idea, so you can probably guess what I think about arrow functions.

Don’t use them as a general replacement for regular functions. They’re more concise, yes, but that brevity comes at the cost of omitting key visual delimiters that help our brains quickly parse out what we’re reading. And, to the point of this discussion, they’re anonymous, which makes them worse for readability from that angle as well.

Arrow functions have a purpose, but that purpose is not to save keystrokes. Arrow functions have lexical this behavior, which is somewhat beyond the bounds of our discussion in this book.

Briefly: arrow functions don’t define a this identifier keyword at all. If you use a this inside an arrow function, it behaves exactly as any other variable reference, which is that the scope chain is consulted to find a function scope (non-arrow function) where it is defined, and to use that one.

In other words, arrow functions treat this like any other lexical variable.

If you’re used to hacks like var self = this, or if you prefer to call .bind(this) on inner function expressions, just to force them to inherit a this from an outer function like it was a lexical variable, then => arrow functions are absolutely the better option. They’re designed specifically to fix that problem.

So, in the rare cases you need lexical this, use an arrow function. It’s the best tool for that job. But just be aware that in doing so, you’re accepting the downsides of an anonymous function. You should expend additional effort to mitigate the readability cost, such as more descriptive variable names and code comments.
