# ch007

## Loops


So it’s clear from our previous discussion that JS doesn’t really want us to “re-declare” our variables within the same scope. That probably seems like a straightforward admonition, until you consider what it means for repeated execution of declaration statements in loops. Consider:

Is value being “re-declared” repeatedly in this program? Will we get errors thrown? No.

All the rules of scope (including “re-declaration” of let-created variables) are applied per scope instance. In other words, each time a scope is entered during execution, everything resets.

Each loop iteration is its own new scope instance, and within each scope instance, value is only being declared once. So there’s no attempted “re-declaration,” and thus no error. Before we consider other loop forms, what if the value declaration in the previous snippet were changed to a var?

Is value being “re-declared” here, especially since we know var allows it? No. Because var is not treated as a block-scoping declaration (see Chapter 6), it attaches itself to the global scope. So there’s just one value variable, in the same scope as keepGoing (global scope, in this case). No “re-declaration” here, either!

One way to keep this all straight is to remember that var, let, and const keywords are effectively removed from the code by the time it starts to execute. They’re handled entirely by the compiler.

If you mentally erase the declarator keywords and then try to process the code, it should help you decide if and when (re-)declarations might occur.

What about “re-declaration” with other loop forms, like for-loops?

It should be clear that there’s only one value declared per scope instance. But what about i? Is it being “re-declared”?

To answer that, consider what scope i is in. It might seem like it would be in the outer (in this case, global) scope, but it’s not. It’s in the scope of for-loop body, just like value is. In fact, you could sorta think about that loop in this more verbose equivalent form:

Now it should be clear: the i and value variables are both declared exactly once per scope instance. No “re-declaration” here.

What about other for-loop forms?

Same thing with for..in and for..of loops: the declared variable is treated as inside the loop body, and thus is handled per iteration (aka, per scope instance). No “re-declaration.”

OK, I know you’re thinking that I sound like a broken record at this point. But let’s explore how const impacts these looping constructs. Consider:

Just like the let variant of this program we saw earlier, const is being run exactly once within each loop iteration, so it’s safe from “re-declaration” troubles. But things get more complicated when we talk about for-loops.

for..in and for..of are fine to use with const:

But not the general for-loop:

What’s wrong here? We could use let just fine in this construct, and we asserted that it creates a new i for each loop iteration scope, so it doesn’t even seem to be a “re-declaration.”

Let’s mentally “expand” that loop like we did earlier:

Do you spot the problem? Our i is indeed just created once inside the loop. That’s not the problem. The problem is the conceptual $$i that must be incremented each time with the $$i++ expression. That’s re-assignment (not “re-declaration”), which isn’t allowed for constants.

Remember, this “expanded” form is only a conceptual model to help you intuit the source of the problem. You might wonder if JS could have effectively made the const $$i = 0 instead into let $ii = 0, which would then allow const to work with our classic for-loop? It’s possible, but then it could have introduced potentially surprising exceptions to for-loop semantics.

For example, it would have been a rather arbitrary (and likely confusing) nuanced exception to allow i++ in the for-loop header to skirt strictness of the const assignment, but not allow other re-assignments of i inside the loop iteration, as is sometimes useful.

The straightforward answer is: const can’t be used with the classic for-loop form because of the required re-assignment.

Interestingly, if you don’t do re-assignment, then it’s valid:

That works, but it’s pointless. There’s no reason to declare i in that position with a const, since the whole point of such a variable in that position is to be used for counting iterations. Just use a different loop form, like a while loop, or use a let!
