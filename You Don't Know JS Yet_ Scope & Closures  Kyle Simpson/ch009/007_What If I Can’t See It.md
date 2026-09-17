# ch009

## What If I Can’t See It?


You’ve probably heard this common adage:

If a tree falls in the forest but nobody is around to hear it, does it make a sound?

It’s a silly bit of philosophical gymnastics. Of course from a scientific perspective, sound waves are created. But the real point: does it matter if the sound happens?

Remember, the emphasis in our definition of closure is observability. If a closure exists (in a technical, implementation, or academic sense) but it cannot be observed in our programs, does it matter? No.

To reinforce this point, let’s look at some examples that are not observably based on closure.

For example, invoking a function that makes use of lexical scope lookup:

The inner function output() accesses the variables greeting and myName from its enclosing scope. But the invocation of output() happens in that same scope, where of course greeting and myName are still available; that’s just lexical scope, not closure.

Any lexically scoped language whose functions didn’t support closure would still behave this same way.

In fact, global scope variables essentially cannot be (observably) closed over, because they’re always accessible from everywhere. No function can ever be invoked in any part of the scope chain that is not a descendant of the global scope.

The inner firstStudent() function does reference students, which is a variable outside its own scope. But since students happens to be from the global scope, no matter where that function is invoked in the program, its ability to access students is nothing more special than normal lexical scope.

All function invocations can access global variables, regardless of whether closure is supported by the language or not. Global variables don’t need to be closed over.

Variables that are merely present but never accessed don’t result in closure:

The inner function nobody() doesn’t close over any outer variables—it only uses its own variable msg. Even though studentID is present in the enclosing scope, studentID is not referred to by nobody(). The JS engine doesn’t need to keep studentID around after lookupStudent(..) has finished running, so GC wants to clean up that memory!

Whether JS functions support closure or not, this program would behave the same. Therefore, no observed closure here.

If there’s no function invocation, closure can’t be observed:

This one’s tricky, because the outer function definitely does get invoked. But the inner function is the one that could have had closure, and yet it’s never invoked; the returned function here is just thrown away. So even if technically the JS engine created closure for a brief moment, it was not observed in any meaningful way in this program.

A tree may have fallen… but we didn’t hear it, so we don’t care.
