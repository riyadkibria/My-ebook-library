# ch011

## Synchronous Callback?


But what about synchronous callbacks? Consider:

Should we refer to formatIDLabel(..) as a callback? Is the map(..) utility really calling back into our program by invoking the function we provided?

There’s nothing to call back into per se, because the program hasn’t paused or exited. We’re passing a function (reference) from one part of the program to another part of the program, and then it’s immediately invoked.

There’s other established terms that might match what we’re doing—passing in a function (reference) so that another part of the program can invoke it on our behalf. You might think of this as Dependency Injection (DI) or Inversion of Control (IoC).

DI can be summarized as passing in necessary part(s) of functionality to another part of the program so that it can invoke them to complete its work. That’s a decent description for the map(..) call above, isn’t it? The map(..) utility knows to iterate over the list’s values, but it doesn’t know what to do with those values. That’s why we pass it the formatIDLabel(..) function. We pass in the dependency.

IoC is a pretty similar, related concept. Inversion of control means that instead of the current area of your program controlling what’s happening, you hand control off to another part of the program. We wrapped the logic for computing a label string in the function formatIDLabel(..), then handed invocation control to the map(..) utility.

Notably, Martin Fowler cites IoC as the difference between a framework and a library: with a library, you call its functions; with a framework, it calls your functions. 1

In the context of our discussion, either DI or IoC could work as an alternative label for a synchronous callback.

But I have a different suggestion. Let’s refer to (the functions formerly known as) synchronous callbacks, as inter-invoked functions (IIFs). Yes, exactly, I’m playing off IIFEs. These kinds of functions are inter-invoked, meaning: another entity invokes them, as opposed to IIFEs, which invoke themselves immediately.

What’s the relationship between an asynchronous callback and an IIF? An asynchronous callback is an IIF that’s invoked asynchronously instead of synchronously.
