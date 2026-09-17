# ch008

## Invoking Function Expressions Immediately


There’s another important bit in the previous factorial recursive program that’s easy to miss: the line at the end of the function expression that contains })();.

Notice that we surrounded the entire function expression in a set of ( .. ), and then on the end, we added that second () parentheses set; that’s actually calling the function expression we just defined. Moreover, in this case, the first set of surrounding ( .. ) around the function expression is not strictly necessary (more on that in a moment), but we used them for readability sake anyway.

So, in other words, we’re defining a function expression that’s then immediately invoked. This common pattern has a (very creative!) name: Immediately Invoked Function Expression (IIFE).

An IIFE is useful when we want to create a scope to hide variables/functions. Since it’s an expression, it can be used in any place in a JS program where an expression is allowed. An IIFE can be named, as with hideTheCache(), or (much more commonly!) unnamed/anonymous. And it can be standalone or, as before, part of another statement—hideTheCache() returns the factorial() function reference which is then = assigned to the variable factorial.

For comparison, here’s an example of a standalone IIFE:

Unlike earlier with hideTheCache(), where the outer surrounding (..) were noted as being an optional stylistic choice, for a standalone IIFE they’re required; they distinguish the function as an expression, not a statement. For consistency, however, always surround an IIFE function with ( .. ).
