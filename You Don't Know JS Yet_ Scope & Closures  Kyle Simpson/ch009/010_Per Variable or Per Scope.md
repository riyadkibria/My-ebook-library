# ch009

## Per Variable or Per Scope?


Another question we need to tackle: should we think of closure as applied only to the referenced outer variable(s), or does closure preserve the entire scope chain with all its variables?

In other words, in the previous event subscription snippet, is the inner onClick(..) function closed over only cb, or is it also closed over clickHandler, clickHandlers, and btn?

Conceptually, closure is per variable rather than per scope. Ajax callbacks, event handlers, and all other forms of function closures are typically assumed to close over only what they explicitly reference.

But the reality is more complicated than that.

Another program to consider:

The outer function manageStudentGrades(..) takes a list of student records, and returns an addGrade(..) function reference, which we externally label addNextGrade(..). Each time we call addNextGrade(..) with a new grade, we get back a current list of the top 10 grades, sorted numerically descending (see sortAndTrimGradesList()).

From the end of the original manageStudentGrades(..) call, and between the multiple addNextGrade(..) calls, the grades variable is preserved inside addGrade(..) via closure; that’s how the running list of top grades is maintained. Remember, it’s a closure over the variable grades itself, not the array it holds.

That’s not the only closure involved, however. Can you spot other variables being closed over?

Did you spot that addGrade(..) references sortAndTrimGradesList? That means it’s also closed over that identifier, which happens to hold a reference to the sortAndTrimGradesList() function. That second inner function has to stay around so that addGrade(..) can keep calling it, which also means any variables it closes over stick around—though, in this case, nothing extra is closed over there.

What else is closed over?

Consider the getGrade variable (and its function); is it closed over? It’s referenced in the outer scope of manageStudentGrades(..) in the .map(getGrade) call. But it’s not referenced in addGrade(..) or sortAndTrimGradesList().

What about the (potentially) large list of student records we pass in as studentRecords? Is that variable closed over? If it is, the array of student records is never getting GC’d, which leads to this program holding onto a larger amount of memory than we might assume. But if we look closely again, none of the inner functions reference studentRecords.

According to the per variable definition of closure, since getGrade and studentRecords are not referenced by the inner functions, they’re not closed over. They should be freely available for GC right after the manageStudentGrades(..) call completes.

Indeed, try debugging this code in a recent JS engine, like v8 in Chrome, placing a breakpoint inside the addGrade(..) function. You may notice that the inspector does not list the studentRecords variable. That’s proof, debugging-wise anyway, that the engine does not maintain studentRecords via closure. Phew!

But how reliable is this observation as proof? Consider this (rather contrived!) program:

Notice that the inner function getInfo(..) is not explicitly closed over any of id, name, or grade variables. And yet, calls to info(..) seem to still be able to access the variables, albeit through use of the eval(..) lexical scope cheat (see Chapter 1).

So all the variables were definitely preserved via closure, despite not being explicitly referenced by the inner function. So does that disprove the per variable assertion in favor of per scope? Depends.

Many modern JS engines do apply an optimization that removes any variables from a closure scope that aren’t explicitly referenced. However, as we see with eval(..), there are situations where such an optimization cannot be applied, and the closure scope continues to contain all its original variables. In other words, closure must be per scope, implementation wise, and then an optional optimization trims down the scope to only what was closed over (a similar outcome as per variable closure).

Even as recent as a few years ago, many JS engines did not apply this optimization; it’s possible your websites may still run in such browsers, especially on older or lower-end devices. That means it’s possible that long-lived closures such as event handlers may be holding onto memory much longer than we would have assumed.

And the fact that it’s an optional optimization in the first place, rather than a requirement of the specification, means that we shouldn’t just casually over-assume its applicability.

In cases where a variable holds a large value (like an object or array) and that variable is present in a closure scope, if you don’t need that value anymore and don’t want that memory held, it’s safer (memory usage) to manually discard the value rather than relying on closure optimization/GC.

Let’s apply a fix to the earlier manageStudentGrades(..) example to ensure the potentially large array held in studentRecords is not caught up in a closure scope unnecessarily:

We’re not removing studentRecords from the closure scope; that we cannot control. We’re ensuring that even if studentRecords remains in the closure scope, that variable is no longer referencing the potentially large array of data; the array can be GC’d.

Again, in many cases JS might automatically optimize the program to the same effect. But it’s still a good habit to be careful and explicitly make sure we don’t keep any significant amount of device memory tied up any longer than necessary.

As a matter of fact, we also technically don’t need the function getGrade() anymore after the .map(getGrade) call completes. If profiling our application showed this was a critical area of excess memory use, we could possibly eek out a tiny bit more memory by freeing up that reference so its value isn’t tied up either. That’s likely unnecessary in this toy example, but this is a general technique to keep in mind if you’re optimizing the memory footprint of your application.

The takeaway: it’s important to know where closures appear in our programs, and what variables are included. We should manage these closures carefully so we’re only holding onto what’s minimally needed and not wasting memory.
