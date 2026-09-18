# Everything Is Concurrent


**Source File:**

None


**Word Count:**

None



---

It’s almost impossible to write code in a decent-sized system that doesn’t have concurrent aspects to it. They may be explicit, or they may be buried inside a library. Concurrency is a requirement if you want your application to be able to deal with the real world, where things are asynchronous: users are interacting, data is being fetched, external services are being called, all at the same time. If you force this process to be serial, with one thing happening, then the next, and so on, your system feels sluggish and you’re probably not taking full advantage of the power of the hardware on which it runs.

In this chapter we’ll look at concurrency and parallelism.

Developers often talk about coupling between chunks of code. They’re referring to dependencies, and how those dependencies make things hard to change. But there’s another form of coupling. Temporal coupling happens when your code imposes a sequence on things that is not required to solve the problem at hand. Do you depend on the “tick” coming before the “tock”? Not if you want to stay flexible. Does your code access multiple back-end services sequentially, one after the other? Not if you want to keep your customers. In Topic 33, ​ Breaking Temporal Coupling ​ , we’ll look at ways of identifying this kind of temporal coupling.

Temporal coupling

Why is writing concurrent and parallel code so difficult? One reason is that we learned to program using sequential systems, and our languages have features that are relatively safe when used sequentially but become a liability once two things can happen at the same time. One of the biggest culprits here is shared state . This doesn’t just mean global variables: any time two or more chunks of code hold references to the same piece of mutable data, you have shared state. And Topic 34, ​ Shared State Is Incorrect State ​ . The section describes a number of workarounds for this, but ultimately they’re all error prone.

shared state

If that makes you feel sad, nil desperandum! There are better ways to construct concurrent applications. One of these is using the actor model , where independent processes, which share no data, communicate over channels using defined, simple, semantics. We talk about both the theory and practice of this approach in Topic 35, ​ Actors and Processes ​ .

nil desperandum!

actor model

Finally, we’ll look at Topic 36, ​ Blackboards ​ . These are systems which act like a combination of an object store and a smart publish/subscribe broker. In their original form, they never really took off. But today we’re seeing more and more implementations of middleware layers with blackboard-like semantics. Used correctly, these types of systems offer a serious amount of decoupling.

Concurrent and parallel code used to be exotic. Now it is required.

