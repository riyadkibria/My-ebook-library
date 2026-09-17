# ch007

## Constants?


The const keyword is more constrained than let. Like let, const cannot be repeated with the same identifier in the same scope. But there’s actually an overriding technical reason why that sort of “re-declaration” is disallowed, unlike let which disallows “re-declaration” mostly for stylistic reasons.

The const keyword requires a variable to be initialized, so omitting an assignment from the declaration results in a SyntaxError:

const declarations create variables that cannot be re-assigned:

The studentName variable cannot be re-assigned because it’s declared with a const.

So if const declarations cannot be re-assigned, and const declarations always require assignments, then we have a clear technical reason why const must disallow any “re-declarations”: any const “re-declaration” would also necessarily be a const re-assignment, which can’t be allowed!

Since const “re-declaration” must be disallowed (on those technical grounds), TC39 essentially felt that let “re-declaration” should be disallowed as well, for consistency. It’s debatable if this was the best choice, but at least we have the reasoning behind the decision.
