# ch011

## const-antly Confused


const on the other hand, I don’t use as often. I’m not going to dig into all the reasons why, but it comes down to const not carrying its own weight. That is, while there’s a tiny bit of benefit of const in some cases, that benefit is outweighed by the long history of troubles around const confusion in a variety of languages, long before it ever showed up in JS.

const pretends to create values that can’t be mutated—a misconception that’s extremely common in developer communities across many languages—whereas what it really does is prevent re-assignment.

Using a const with a mutable value (like an array or object) is asking for a future developer (or reader of your code) to fall into the trap you set, which was that they either didn’t know, or sorta forgot, that value immutability isn’t at all the same thing as assignment immutability.

I just don’t think we should set those traps. The only time I ever use const is when I’m assigning an already-immutable value (like 42 or "Hello, friends!"), and when it’s clearly a “constant” in the sense of being a named placeholder for a literal value, for semantic purposes. That’s what const is best used for. That’s pretty rare in my code, though.

If variable re-assignment were a big deal, then const would be more useful. But variable re-assignment just isn’t that big of a deal in terms of causing bugs. There’s a long list of things that lead to bugs in programs, but “accidental re-assignment” is way, way down that list.

Combine that with the fact that const (and let) are supposed to be used in blocks, and blocks are supposed to be short, and you have a really small area of your code where a const declaration is even applicable. A const on line 1 of your ten-line block only tells you something about the next nine lines. And the thing it tells you is already obvious by glancing down at those nine lines: the variable is never on the left-hand side of an =; it’s not re-assigned.

That’s it, that’s all const really does. Other than that, it’s not very useful. Stacked up against the significant confusion of value vs. assignment immutability, const loses a lot of its luster.

A let (or var!) that’s never re-assigned is already behaviorally a “constant”, even though it doesn’t have the compiler guarantee. That’s good enough in most cases.
