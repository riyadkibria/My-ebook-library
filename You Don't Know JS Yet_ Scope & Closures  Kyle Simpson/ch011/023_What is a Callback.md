# ch011

## What is a Callback?


Before we revisit closure, let me spend a brief moment addressing the word “callback.” It’s a generally accepted norm that saying “callback” is synonymous with both asynchronous callbacks and synchronous callbacks. I don’t think I agree that this is a good idea, so I want to explain why and propose we move away from that to another term.

Let’s first consider an asynchronous callback, a function reference that will be invoked at some future later point. What does “callback” mean, in this case?

It means that the current code has finished or paused, suspended itself, and that when the function in question is invoked later, execution is entering back into the suspended program, resuming it. Specifically, the point of re-entry is the code that was wrapped in the function reference:

In this context, “calling back” makes a lot of sense. The JS engine is resuming our suspended program by calling back in at a specific location. OK, so a callback is asynchronous.
