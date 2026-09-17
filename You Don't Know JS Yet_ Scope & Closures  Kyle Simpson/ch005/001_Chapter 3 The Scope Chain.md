# ch005

## Chapter 3: The Scope Chain


Chapters 1 and 2 laid down a concrete definition of lexical scope (and its parts) and illustrated helpful metaphors for its conceptual foundation. Before proceeding with this chapter, find someone else to explain (written or aloud), in your own words, what lexical scope is and why it’s useful to understand.

That seems like a step you might skip, but I’ve found it really does help to take the time to reformulate these ideas as explanations to others. That helps our brains digest what we’re learning!

Now it’s time to dig into the nuts and bolts, so expect that things will get a lot more detailed from here forward. Stick with it, though, because these discussions really hammer home just how much we all don’t know about scope, yet. Make sure to take your time with the text and all the code snippets provided.

To refresh the context of our running example, let’s recall the color-coded illustration of the nested scope bubbles, from Chapter 2, Figure 2:

The connections between scopes that are nested within other scopes is called the scope chain, which determines the path along which variables can be accessed. The chain is directed, meaning the lookup moves upward/outward only.
