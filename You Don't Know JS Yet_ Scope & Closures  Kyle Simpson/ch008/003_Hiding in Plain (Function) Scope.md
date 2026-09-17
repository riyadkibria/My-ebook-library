# ch008

## Hiding in Plain (Function) Scope


It should now be clear why it’s important to hide our variable and function declarations in the lowest (most deeply nested) scopes possible. But how do we do so?

We’ve already seen the let and const keywords, which are block scoped declarators; we’ll come back to them in more detail shortly. But first, what about hiding var or function declarations in scopes? That can easily be done by wrapping a function scope around a declaration.

Let’s consider an example where function scoping can be useful.

The mathematical operation “factorial” (notated as “6!”) is the multiplication of a given integer against all successively lower integers down to 1—actually, you can stop at 2 since multiplying 1 does nothing. In other words, “6!” is the same as “6 * 5!”, which is the same as “6 * 5 * 4!”, and so on. Because of the nature of the math involved, once any given integer’s factorial (like “4!”) has been calculated, we shouldn’t need to do that work again, as it’ll always be the same answer.

So if you naively calculate factorial for 6, then later want to calculate factorial for 7, you might unnecessarily re-calculate the factorials of all the integers from 2 up to 6. If you’re willing to trade memory for speed, you can solve that wasted computation by caching each integer’s factorial as it’s calculated:

We’re storing all the computed factorials in cache so that across multiple calls to factorial(..), the previous computations remain. But the cache variable is pretty obviously a private detail of how factorial(..) works, not something that should be exposed in an outer scope—especially not the global scope.

However, fixing this over-exposure issue is not as simple as hiding the cache variable inside factorial(..), as it might seem. Since we need cache to survive multiple calls, it must be located in a scope outside that function. So what can we do?

Define another middle scope (between the outer/global scope and the inside of factorial(..)) for cache to be located:

The hideTheCache() function serves no other purpose than to create a scope for cache to persist in across multiple calls to factorial(..). But for factorial(..) to have access to cache, we have to define factorial(..) inside that same scope. Then we return the function reference, as a value from hideTheCache(), and store it in an outer scope variable, also named factorial. Now as we call factorial(..) (multiple times!), its persistent cache stays hidden yet accessible only to factorial(..)!

OK, but… it’s going to be tedious to define (and name!) a hideTheCache(..) function scope each time such a need for variable/function hiding occurs, especially since we’ll likely want to avoid name collisions with this function by giving each occurrence a unique name. Ugh.

Rather than defining a new and uniquely named function each time one of those scope-only-for-the-purpose-of-hiding-a-variable situations occurs, a perhaps better solution is to use a function expression:

Wait! This is still using a function to create the scope for hiding cache, and in this case, the function is still named hideTheCache, so how does that solve anything?

Recall from “Function Name Scope” (in Chapter 3), what happens to the name identifier from a function expression. Since hideTheCache(..) is defined as a function expression instead of a function declaration, its name is in its own scope—essentially the same scope as cache—rather than in the outer/global scope.

That means we can name every single occurrence of such a function expression the exact same name, and never have any collision. More appropriately, we can name each occurrence semantically based on whatever it is we’re trying to hide, and not worry that whatever name we choose is going to collide with any other function expression scope in the program.

In fact, we could just leave off the name entirely—thus defining an “anonymous function expression” instead. But Appendix A will discuss the importance of names even for such scope-only functions.
