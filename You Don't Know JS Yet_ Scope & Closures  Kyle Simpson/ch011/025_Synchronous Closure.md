# ch011

## Synchronous Closure?


Now that we’ve re-labeled synchronous callbacks as IIFs, we can return to our main question: are IIFs an example of closure? Obviously, the IIF would have to reference variable(s) from an outer scope for it to have any chance of being a closure. The formatIDLabel(..) IIF from earlier does not reference any variables outside its own scope, so it’s definitely not a closure.

What about an IIF that does have external references, is that closure?

The inner renderLabel(..) IIF references list from the enclosing scope, so it’s an IIF that could have closure. But here’s where the definition/model we choose for closure matters:

If renderLabel(..) is a function that gets passed somewhere else, and that function is then invoked, then yes, renderLabel(..) is exercising a closure, because closure is what preserved its access to its original scope chain.

But if, as in the alternative conceptual model from Chapter 7, renderLabel(..) stays in place, and only a reference to it is passed to forEach(..), is there any need for closure to preserve the scope chain of renderLabel(..), while it executes synchronously right inside its own scope?

No. That’s just normal lexical scope.

To understand why, consider this alternative form of printLabels(..):

These two versions of printLabels(..) are essentially the same.

The latter one is definitely not an example of closure, at least not in any useful or observable sense. It’s just lexical scope. The former version, with forEach(..) calling our function reference, is essentially the same thing. It’s also not closure, but rather just a plain ol’ lexical scope function call.
