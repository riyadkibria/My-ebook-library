# ch011

## Are Synchronous Callbacks Still Closures?


Chapter 7 presented two different models for tackling closure:

Closure is a function instance remembering its outer variables even as that function is passed around and invoked in other scopes.

Closure is a function instance and its scope environment being preserved in-place while any references to it are passed around and invoked from other scopes.

These models are not wildly divergent, but they do approach from a different perspective. And that different perspective changes what we identify as a closure.

Don’t get lost following this rabbit trail through closures and callbacks:
