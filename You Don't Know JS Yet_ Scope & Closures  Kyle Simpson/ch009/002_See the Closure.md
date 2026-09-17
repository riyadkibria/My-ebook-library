# ch009

## See the Closure


Closure is originally a mathematical concept, from lambda calculus. But I’m not going to list out math formulas or use a bunch of notation and jargon to define it.

Instead, I’m going to focus on a practical perspective. We’ll start by defining closure in terms of what we can observe in different behavior of our programs, as opposed to if closure was not present in JS. However, later in this chapter, we’re going to flip closure around to look at it from an alternative perspective.

Closure is a behavior of functions and only functions. If you aren’t dealing with a function, closure does not apply. An object cannot have closure, nor does a class have closure (though its functions/methods might). Only functions have closure.

For closure to be observed, a function must be invoked, and specifically it must be invoked in a different branch of the scope chain from where it was originally defined. A function executing in the same scope it was defined would not exhibit any observably different behavior with or without closure being possible; by the observational perspective and definition, that is not closure.

Let’s look at some code, annotated with its relevant scope bubble colors (see Chapter 2):

The first thing to notice about this code is that the lookupStudent(..) outer function creates and returns an inner function called greetStudent(..). lookupStudent(..) is called twice, producing two separate instances of its inner greetStudent(..) function, both of which are saved into the chosenStudents array.

We verify that’s the case by checking the .name property of the returned function saved in chosenStudents[0], and it’s indeed an instance of the inner greetStudent(..).

After each call to lookupStudent(..) finishes, it would seem like all its inner variables would be discarded and GC’d (garbage collected). The inner function is the only thing that seems to be returned and preserved. But here’s where the behavior differs in ways we can start to observe.

While greetStudent(..) does receive a single argument as the parameter named greeting, it also makes reference to both students and studentID, identifiers which come from the enclosing scope of lookupStudent(..). Each of those references from the inner function to the variable in an outer scope is called a closure. In academic terms, each instance of greetStudent(..) closes over the outer variables students and studentID.

So what do those closures do here, in a concrete, observable sense?

Closure allows greetStudent(..) to continue to access those outer variables even after the outer scope is finished (when each call to lookupStudent(..) completes). Instead of the instances of students and studentID being GC’d, they stay around in memory. At a later time when either instance of the greetStudent(..) function is invoked, those variables are still there, holding their current values.

If JS functions did not have closure, the completion of each lookupStudent(..) call would immediately tear down its scope and GC the students and studentID variables. When we later called one of the greetStudent(..) functions, what would then happen?

If greetStudent(..) tried to access what it thought was a BLUE(2) marble, but that marble did not actually exist (anymore), the reasonable assumption is we should get a ReferenceError, right?

But we don’t get an error. The fact that the execution of chosenStudents[0]("Hello") works and returns us the message “Hello, Sarah!”, means it was still able to access the students and studentID variables. This is a direct observation of closure!
