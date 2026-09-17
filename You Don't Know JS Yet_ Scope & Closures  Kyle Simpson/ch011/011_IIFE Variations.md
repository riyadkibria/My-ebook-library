# ch011

## IIFE Variations


All functions should have names. I said that a few times, right!? That includes IIFEs.

How do we come up with a name for an IIFE? Identify what the IIFE is there for. Why do you need a scope in that spot? Are you hiding a cache variable for student records?

I named the IIFE StoreStudentRecords because that’s what it’s doing: storing student records. Every IIFE should have a name. No exceptions.

IIFEs are typically defined by placing ( .. ) around the function expression, as shown in those previous snippets. But that’s not the only way to define an IIFE. Technically, the only reason we’re using that first surrounding set of ( .. ) is just so the function keyword isn’t in a position to qualify as a function declaration to the JS parser. But there are other syntactic ways to avoid being parsed as a declaration:

The !, +, ~, and several other unary operators (operators with one operand) can all be placed in front of function to turn it into an expression. Then the final () call is valid, which makes it an IIFE.

I actually kind of like using the void unary operator when defining a standalone IIFE:

The benefit of void is, it clearly communicates at the beginning of the function that this IIFE won’t be returning any value.

However you define your IIFEs, show them some love by giving them names.
