# ch011

## Who let the TDZ Out?


But that’s just const. What about let?

Well, TC39 made the decision: since we need a TDZ for const, we might as well have a TDZ for let as well. In fact, if we make let have a TDZ, then we discourage all that ugly variable hoisting people do. So there was a consistency perspective and, perhaps, a bit of social engineering to shift developers’ behavior.

My counter-argument would be: if you’re favoring consistency, be consistent with var instead of const; let is definitely more like var than const. That’s especially true since they had already chosen consistency with var for the whole hoisting-to-the-top-of-the-scope thing. Let const be its own unique deal with a TDZ, and let the answer to TDZ purely be: just avoid the TDZ by always declaring your constants at the top of the scope. I think this would have been more reasonable.

But alas, that’s not how it landed. let has a TDZ because const needs a TDZ, because let and const mimic var in their hoisting to the top of the (block) scope. There ya go. Too circular? Read it again a few times.
