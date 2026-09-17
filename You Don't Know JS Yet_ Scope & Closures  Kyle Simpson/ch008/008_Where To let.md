# ch008

## Where To let?


My advice to reserve var for (mostly) only a top-level function scope means that most other declarations should use let. But you may still be wondering how to decide where each declaration in your program belongs?

POLE already guides you on those decisions, but let’s make sure we explicitly state it. The way to decide is not based on which keyword you want to use. The way to decide is to ask, “What is the most minimal scope exposure that’s sufficient for this variable?”

Once that is answered, you’ll know if a variable belongs in a block scope or the function scope. If you decide initially that a variable should be block-scoped, and later realize it needs to be elevated to be function-scoped, then that dictates a change not only in the location of that variable’s declaration, but also the declarator keyword used. The decision-making process really should proceed like that.

If a declaration belongs in a block scope, use let. If it belongs in the function scope, use var (again, just my opinion).

But another way to sort of visualize this decision making is to consider the pre-ES6 version of a program. For example, let’s recall diff(..) from earlier:

In this version of diff(..), tmp is clearly declared in the function scope. Is that appropriate for tmp? I would argue, no. tmp is only needed for those few statements. It’s not needed for the return statement. It should therefore be block-scoped.

Prior to ES6, we didn’t have let so we couldn’t actually block-scope it. But we could do the next-best thing in signaling our intent:

Placing the var declaration for tmp inside the if statement signals to the reader of the code that tmp belongs to that block. Even though JS doesn’t enforce that scoping, the semantic signal still has benefit for the reader of your code.

Following this perspective, you can find any var that’s inside a block of this sort and switch it to let to enforce the semantic signal already being sent. That’s proper usage of let in my opinion.

Another example that was historically based on var but which should now pretty much always use let is the for loop:

No matter where such a loop is defined, the i should basically always be used only inside the loop, in which case POLE dictates it should be declared with let instead of var:

Almost the only case where switching a var to a let in this way would “break” your code is if you were relying on accessing the loop’s iterator (i) outside/after the loop, such as:

This usage pattern is not terribly uncommon, but most feel it smells like poor code structure. A preferable approach is to use another outer-scoped variable for that purpose:

lastI is needed across this whole scope, so it’s declared with var. i is only needed in (each) loop iteration, so it’s declared with let.
