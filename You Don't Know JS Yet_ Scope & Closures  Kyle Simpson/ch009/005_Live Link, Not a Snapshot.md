# ch009

## Live Link, Not a Snapshot


In both examples from the previous sections, we read the value from a variable that was held in a closure. That makes it feel like closure might be a snapshot of a value at some given moment. Indeed, that’s a common misconception.

Closure is actually a live link, preserving access to the full variable itself. We’re not limited to merely reading a value; the closed-over variable can be updated (re-assigned) as well! By closing over a variable in a function, we can keep using that variable (read and write) as long as that function reference exists in the program, and from anywhere we want to invoke that function. This is why closure is such a powerful technique used widely across so many areas of programming!

Figure 4 depicts the function instances and scope links:

As shown in Figure 4, each call to adder(..) creates a new BLUE(2) scope containing a num1 variable, as well as a new instance of addTo(..) function as a GREEN(3) scope. Notice that the function instances (addTo10(..) and addTo42(..)) are present in and invoked from the RED(1) scope.

Now let’s examine an example where the closed-over variable is updated:

The count variable is closed over by the inner getCurrent() function, which keeps it around instead of it being subjected to GC. The hits() function calls access and update this variable, returning an incrementing count each time.

Though the enclosing scope of a closure is typically from a function, that’s not actually required; there only needs to be an inner function present inside an outer scope:

Because it’s so common to mistake closure as value-oriented instead of variable-oriented, developers sometimes get tripped up trying to use closure to snapshot-preserve a value from some moment in time. Consider:

By defining greeting() (aka, hello()) when studentName holds the value "Frank" (before the re-assignment to "Suzy"), the mistaken assumption is often that the closure will capture "Frank". But greeting() is closed over the variable studentName, not its value. Whenever greeting() is invoked, the current value of the variable ("Suzy", in this case) is reflected.

The classic illustration of this mistake is defining functions inside a loop:

You might have expected the keeps[0]() invocation to return 0, since that function was created during the first iteration of the loop when i was 0. But again, that assumption stems from thinking of closure as value-oriented rather than variable-oriented.

Something about the structure of a for-loop can trick us into thinking that each iteration gets its own new i variable; in fact, this program only has one i since it was declared with var.

Each saved function returns 3, because by the end of the loop, the single i variable in the program has been assigned 3. Each of the three functions in the keeps array do have individual closures, but they’re all closed over that same shared i variable.

Of course, a single variable can only ever hold one value at any given moment. So if you want to preserve multiple values, you need a different variable for each.

How could we do that in the loop snippet? Let’s create a new variable for each iteration:

Each function is now closed over a separate (new) variable from each iteration, even though all of them are named j. And each j gets a copy of the value of i at that point in the loop iteration; that j never gets re-assigned. So all three functions now return their expected values: 0, 1, and 2!

Again remember, even if we were using asynchrony in this program, such as passing each inner keepEachJ() function into setTimeout(..) or some event handler subscription, the same kind of closure behavior would still be observed.

Recall the “Loops” section in Chapter 5, which illustrates how a let declaration in a for loop actually creates not just one variable for the loop, but actually creates a new variable for each iteration of the loop. That trick/quirk is exactly what we need for our loop closures:

Since we’re using let, three i’s are created, one for each loop, so each of the three closures just work as expected.
