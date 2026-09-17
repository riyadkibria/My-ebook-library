# ch011

## Defer to Closure


By the way, Chapter 7 briefly mentioned partial application and currying (which do rely on closure!). This is a interesting scenario where manual currying can be used:

The inner function createLabel(..), which we assign to renderLabel, is closed over list, so closure is definitely being utilized.

Closure allows us to remember list for later, while we defer execution of the actual label-creation logic from the renderTo(..) call to the subsequent forEach(..) invocations of the createLabel(..) IIF. That may only be a brief moment here, but any amount of time could pass, as closure bridges from call to call.
