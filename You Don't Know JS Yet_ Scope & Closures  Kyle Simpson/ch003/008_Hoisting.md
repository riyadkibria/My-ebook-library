# ch003

## Hoisting


The noted ReferenceError occurs from the line with the statement greeting = "Howdy". What’s happening is that the greeting variable for that statement belongs to the declaration on the next line, let greeting = "Hi", rather than to the previous var greeting = "Hello" statement.

The only way the JS engine could know, at the line where the error is thrown, that the next statement would declare a block-scoped variable of the same name (greeting) is if the JS engine had already processed this code in an earlier pass, and already set up all the scopes and their variable associations. This processing of scopes and declarations can only accurately be accomplished by parsing the program before execution.

The ReferenceError here technically comes from greeting = "Howdy" accessing the greeting variable too early, a conflict referred to as the Temporal Dead Zone (TDZ). Chapter 5 will cover this in more detail.

Hopefully you’re now convinced that JS programs are parsed before any execution begins. But does it prove they are compiled?

This is an interesting question to ponder. Could JS parse a program, but then execute that program by interpreting operations represented in the AST without first compiling the program? Yes, that is possible. But it’s extremely unlikely, mostly because it would be extremely inefficient performance wise.

It’s hard to imagine a production-quality JS engine going to all the trouble of parsing a program into an AST, but not then converting (aka, “compiling”) that AST into the most efficient (binary) representation for the engine to then execute.

Many have endeavored to split hairs with this terminology, as there’s plenty of nuance and “well, actually…” interjections floating around. But in spirit and in practice, what the engine is doing in processing JS programs is much more alike compilation than not.

Classifying JS as a compiled language is not concerned with the distribution model for its binary (or byte-code) executable representations, but rather in keeping a clear distinction in our minds about the phase where JS code is processed and analyzed; this phase observably and indisputedly happens before the code starts to be executed.

We need proper mental models of how the JS engine treats our code if we want to understand JS and scope effectively.
