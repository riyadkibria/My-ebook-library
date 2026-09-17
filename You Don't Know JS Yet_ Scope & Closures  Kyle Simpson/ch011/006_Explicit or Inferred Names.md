# ch011

## Explicit or Inferred Names?


Every function in your program has a purpose. If it doesn’t have a purpose, take it out, because you’re just wasting space. If it does have a purpose, there is a name for that purpose.

So far many readers likely agree with me. But does that mean we should always put that name into the code? Here’s where I’ll raise more than a few eyebrows. I say, unequivocally, yes!

First of all, “anonymous” showing up in stack traces is just not all that helpful to debugging:

Ugh. Compare to what is reported if I give the functions names:

See how waitAMoment and allUpper names appear and give the stack trace more useful information/context for debugging? The program is more debuggable if we use reasonable names for all our functions.

By the way, let’s make sure we’re on the same page about what a named function is:

“But wait!”, you say. Some of those are named, right!?

These are referred to as inferred names. Inferred names are fine, but they don’t really address the full concern I’m discussing.
