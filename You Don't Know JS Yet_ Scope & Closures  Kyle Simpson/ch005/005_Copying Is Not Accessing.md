# ch005

## Copying Is Not Accessing


I’ve been asked the following “But what about…?” question dozens of times. Consider:

Oh! So does this another object technique disprove my claim that the special parameter is “completely inaccessible” from inside keepLooking()? No, the claim is still correct.

special: special is copying the value of the special parameter variable into another container (a property of the same name). Of course, if you put a value in another container, shadowing no longer applies (unless another was shadowed, too!). But that doesn’t mean we’re accessing the parameter special; it means we’re accessing the copy of the value it had at that moment, by way of another container (object property). We cannot reassign the BLUE(2) special parameter to a different value from inside keepLooking().

Another “But…!?” you may be about to raise: what if I’d used objects or arrays as the values instead of the numbers (112358132134, etc.)? Would us having references to objects instead of copies of primitive values “fix” the inaccessibility?

No. Mutating the contents of the object value via a reference copy is not the same thing as lexically accessing the variable itself. We still can’t reassign the BLUE(2) special parameter.
