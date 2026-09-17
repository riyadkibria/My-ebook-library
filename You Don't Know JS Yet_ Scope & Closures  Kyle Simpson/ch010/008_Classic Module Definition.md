# ch010

## Classic Module Definition


So to clarify what makes something a classic module:

There must be an outer scope, typically from a module factory function running at least once.

The module’s inner scope must have at least one piece of hidden information that represents state for the module.

The module must return on its public API a reference to at least one function that has closure over the hidden module state (so that this state is actually preserved).

You’ll likely run across other variations on this classic module approach, which we’ll look at in more detail in Appendix A.
