# ch009

## Common Closures: Ajax and Events


Closure is most commonly encountered with callbacks:

The onRecord(..) callback is going to be invoked at some point in the future, after the response from the Ajax call comes back. This invocation will happen from the internals of the ajax(..) utility, wherever that comes from. Furthermore, when that happens, the lookupStudentRecord(..) call will long since have completed.

Why then is studentID still around and accessible to the callback? Closure.

Event handlers are another common usage of closure:

The label parameter is closed over by the onClick(..) event handler callback. When the button is clicked, label still exists to be used. This is closure.
