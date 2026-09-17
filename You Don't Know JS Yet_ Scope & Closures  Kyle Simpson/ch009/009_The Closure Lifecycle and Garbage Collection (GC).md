# ch009

## The Closure Lifecycle and Garbage Collection (GC)


Since closure is inherently tied to a function instance, its closure over a variable lasts as long as there is still a reference to that function.

If ten functions all close over the same variable, and over time nine of these function references are discarded, the lone remaining function reference still preserves that variable. Once that final function reference is discarded, the last closure over that variable is gone, and the variable itself is GC’d.

This has an important impact on building efficient and performant programs. Closure can unexpectedly prevent the GC of a variable that you’re otherwise done with, which leads to run-away memory usage over time. That’s why it’s important to discard function references (and thus their closures) when they’re not needed anymore.

In this program, the inner onClick(..) function holds a closure over the passed in cb (the provided event callback). That means the checkout() and trackAction() function expression references are held via closure (and cannot be GC’d) for as long as these event handlers are subscribed.

When we call onSubmit() with no input on the last line, all event handlers are unsubscribed, and the clickHandlers array is emptied. Once all click handler function references are discarded, the closures of cb references to checkout() and trackAction() are discarded.

When considering the overall health and efficiency of the program, unsubscribing an event handler when it’s no longer needed can be even more important than the initial subscription!
