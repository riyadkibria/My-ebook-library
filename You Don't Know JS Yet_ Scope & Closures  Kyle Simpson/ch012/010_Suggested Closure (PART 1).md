# ch012

## Suggested: Closure (PART 1)


The Closure Exercise (PART 1) for isPrime(..) and factorize(..), can be solved like this:

The general steps I used for each utility:

Wrap an IIFE to define the scope for the cache variable to reside.

In the underlying call, first check the cache, and if a result is already known, return.

At each place where a return was happening originally, assign to the cache and just return the results of that assignment operation—this is a space savings trick mostly just for brevity in the book.

I also renamed the inner function from factorize(..) to findFactors(..). That’s not technically necessary, but it helps it make clearer which function the recursive calls invoke.
