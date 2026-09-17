# ch008

## Scoping with Blocks


You should by this point feel fairly comfortable with the merits of creating scopes to limit identifier exposure.

So far, we looked at doing this via function (i.e., IIFE) scope. But let’s now consider using let declarations with nested blocks. In general, any { .. } curly-brace pair which is a statement will act as a block, but not necessarily as a scope.

A block only becomes a scope if necessary, to contain its block-scoped declarations (i.e., let or const). Consider:

Not all { .. } curly-brace pairs create blocks (and thus are eligible to become scopes):

Object literals use { .. } curly-brace pairs to delimit their key-value lists, but such object values are not scopes.

class uses { .. } curly-braces around its body definition, but this is not a block or scope.

A function uses { .. } around its body, but this is not technically a block—it’s a single statement for the function body. It is, however, a (function) scope.

The { .. } curly-brace pair on a switch statement (around the set of case clauses) does not define a block/scope.

Other than such non-block examples, a { .. } curly-brace pair can define a block attached to a statement (like an if or for), or stand alone by itself—see the outermost { .. } curly brace pair in the previous snippet. An explicit block of this sort—if it has no declarations, it’s not actually a scope—serves no operational purpose, though it can still be useful as a semantic signal.

Explicit standalone { .. } blocks have always been valid JS syntax, but since they couldn’t be a scope prior to ES6’s let/const, they are quite rare. However, post ES6, they’re starting to catch on a little bit.

In most languages that support block scoping, an explicit block scope is an extremely common pattern for creating a narrow slice of scope for one or a few variables. So following the POLE principle, we should embrace this pattern more widespread in JS as well; use (explicit) block scoping to narrow the exposure of identifiers to the minimum practical.

An explicit block scope can be useful even inside of another block (whether the outer block is a scope or not).

Here, the { .. } curly-brace pair inside the if statement is an even smaller inner explicit block scope for msg, since that variable is not needed for the entire if block. Most developers would just block-scope msg to the if block and move on. And to be fair, when there’s only a few lines to consider, it’s a toss-up judgement call. But as code grows, these over-exposure issues become more pronounced.

So does it matter enough to add the extra { .. } pair and indentation level? I think you should follow POLE and always (within reason!) define the smallest block for each variable. So I recommend using the extra explicit block scope as shown.

Recall the discussion of TDZ errors from “Uninitialized Variables (TDZ)” (Chapter 5). My suggestion there was: to minimize the risk of TDZ errors with let/const declarations, always put those declarations at the top of their scope.

If you find yourself placing a let declaration in the middle of a scope, first think, “Oh, no! TDZ alert!” If this let declaration isn’t needed in the first half of that block, you should use an inner explicit block scope to further narrow its exposure!

Another example with an explicit block scope:

Let’s first identify the scopes and their identifiers:

The outer/global scope has one identifier, the function getNextMonthStart(..).

The function scope for getNextMonthStart(..) has three: dateStr (parameter), nextMonth, and year.

The { .. } curly-brace pair defines an inner block scope that includes one variable: curMonth.

So why put curMonth in an explicit block scope instead of just alongside nextMonth and year in the top-level function scope? Because curMonth is only needed for those first two statements; at the function scope level it’s over-exposed.

This example is small, so the hazards of over-exposing curMonth are pretty limited. But the benefits of the POLE principle are best achieved when you adopt the mindset of minimizing scope exposure by default, as a habit. If you follow the principle consistently even in the small cases, it will serve you more as your programs grow.

Let’s now look at an even more substantial example:

There are six identifiers declared across five different scopes. Could all of these variables have existed in the single outer/global scope? Technically, yes, since they’re all uniquely named and thus have no name collisions. But this would be really poor code organization, and would likely lead to both confusion and future bugs.

We split them out into each inner nested scope as appropriate. Each variable is defined at the innermost scope possible for the program to operate as desired.

sortedNames could have been defined in the top-level function scope, but it’s only needed for the second half of this function. To avoid over-exposing that variable in a higher level scope, we again follow POLE and block-scope it in the inner explicit block scope.
