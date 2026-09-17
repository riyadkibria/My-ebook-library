# ch012

## Closure (PART 1)


Let’s first practice closure with some common computer-math operations: determining if a value is prime (has no divisors other than 1 and itself), and generating a list of prime factors (divisors) for a given number.

Here’s an implementation of isPrime(..), adapted from the Math.js library: 1

And here’s a somewhat basic implementation of factorize(..) (not to be confused with factorial(..) from Chapter 6):

If you were to call isPrime(4327) multiple times in a program, you can see that it would go through all its dozens of comparison/computation steps every time. If you consider factorize(..), it’s calling isPrime(..) many times as it computes the list of factors. And there’s a good chance most of those calls are repeats. That’s a lot of wasted work!

The first part of this exercise is to use closure to implement a cache to remember the results of isPrime(..), so that the primality (true or false) of a given number is only ever computed once. Hint: we already showed this sort of caching in Chapter 6 with factorial(..).

If you look at factorize(..), it’s implemented with recursion, meaning it calls itself repeatedly. That again means we may likely see a lot of wasted calls to compute prime factors for the same number. So the second part of the exercise is to use the same closure cache technique for factorize(..).

Use separate closures for caching of isPrime(..) and factorize(..), rather than putting them inside a single scope.

Try the exercise for yourself, then check out the suggested solution at the end of this appendix.
