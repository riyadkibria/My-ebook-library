# ch009

## Adding Up Closures


Let’s examine one of the canonical examples often cited for closure:

Each instance of the inner addTo(..) function is closing over its own num1 variable (with values 10 and 42, respectively), so those num1’s don’t go away just because adder(..) finishes. When we later invoke one of those inner addTo(..) instances, such as the add10To(15) call, its closed-over num1 variable still exists and still holds the original 10 value. The operation is thus able to perform 10 + 15 and return the answer 25.

An important detail might have been too easy to gloss over in that previous paragraph, so let’s reinforce it: closure is associated with an instance of a function, rather than its single lexical definition. In the preceding snippet, there’s just one inner addTo(..) function defined inside adder(..), so it might seem like that would imply a single closure.

But actually, every time the outer adder(..) function runs, a new inner addTo(..) function instance is created, and for each new instance, a new closure. So each inner function instance (labeled add10To(..) and add42To(..) in our program) has its own closure over its own instance of the scope environment from that execution of adder(..).

Even though closure is based on lexical scope, which is handled at compile time, closure is observed as a runtime characteristic of function instances.
