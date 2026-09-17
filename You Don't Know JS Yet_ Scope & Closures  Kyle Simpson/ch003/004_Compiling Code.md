# ch003

## Compiling Code


But first, why does it even matter whether JS is compiled or not?

Scope is primarily determined during compilation, so understanding how compilation and execution relate is key in mastering scope.

In classic compiler theory, a program is processed by a compiler in three basic stages:

Tokenizing/Lexing: breaking up a string of characters into meaningful (to the language) chunks, called tokens. For instance, consider the program: var a = 2;. This program would likely be broken up into the following tokens: var, a, =, 2, and ;. Whitespace may or may not be persisted as a token, depending on whether it’s meaningful or not.

(The difference between tokenizing and lexing is subtle and academic, but it centers on whether or not these tokens are identified in a stateless or stateful way. Put simply, if the tokenizer were to invoke stateful parsing rules to figure out whether a should be considered a distinct token or just part of another token, that would be lexing.)

Parsing: taking a stream (array) of tokens and turning it into a tree of nested elements, which collectively represent the grammatical structure of the program. This is called an Abstract Syntax Tree (AST).

For example, the tree for var a = 2; might start with a top-level node called VariableDeclaration, with a child node called Identifier (whose value is a), and another child called AssignmentExpression which itself has a child called NumericLiteral (whose value is 2).

Code Generation: taking an AST and turning it into executable code. This part varies greatly depending on the language, the platform it’s targeting, and other factors.

The JS engine takes the just described AST for var a = 2; and turns it into a set of machine instructions to actually create a variable called a (including reserving memory, etc.), and then store a value into a.

The JS engine is vastly more complex than just these three stages. In the process of parsing and code generation, there are steps to optimize the performance of the execution (i.e., collapsing redundant elements). In fact, code can even be re-compiled and re-optimized during the progression of execution.

So, I’m painting only with broad strokes here. But you’ll see shortly why these details we do cover, even at a high level, are relevant.

JS engines don’t have the luxury of an abundance of time to perform their work and optimizations, because JS compilation doesn’t happen in a build step ahead of time, as with other languages. It usually must happen in mere microseconds (or less!) right before the code is executed. To ensure the fastest performance under these constraints, JS engines use all kinds of tricks (like JITs, which lazy compile and even hot re-compile); these are well beyond the “scope” of our discussion here.
