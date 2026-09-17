# ch011

## var and let


In my mind, const is pretty rarely useful, so this is only two-horse race between let and var. But it’s not really a race either, because there doesn’t have to be just one winner. They can both win… different races.

The fact is, you should be using both var and let in your programs. They are not interchangeable: you shouldn’t use var where a let is called for, but you also shouldn’t use let where a var is most appropriate.

So where should we still use var? Under what circumstances is it a better choice than let?

For one, I always use var in the top-level scope of any function, regardless of whether that’s at the beginning, middle, or end of the function. I also use var in the global scope, though I try to minimize usage of the global scope.

Why use var for function scoping? Because that’s exactly what var does. There literally is no better tool for the job of function scoping a declaration than a declarator that has, for 25 years, done exactly that.

You could use let in this top-level scope, but it’s not the best tool for that job. I also find that if you use let everywhere, then it’s less obvious which declarations are designed to be localized and which ones are intended to be used throughout the function.

By contrast, I rarely use a var inside a block. That’s what let is for. Use the best tool for the job. If you see a let, it tells you that you’re dealing with a localized declaration. If you see var, it tells you that you’re dealing with a function-wide declaration. Simple as that.

The studentRecords variable is intended for use across the whole function. var is the best declarator to tell the reader that. By contrast, record and id are intended for use only in the narrower scope of the loop iteration, so let is the best tool for that job.

In addition to this best tool semantic argument, var has a few other characteristics that, in certain limited circumstances, make it more powerful.

One example is when a loop is exclusively using a variable, but its conditional clause cannot see block-scoped declarations inside the iteration:

Here, result is clearly only used inside the block, so we use let. But done is a bit different. It’s only useful for the loop, but the while clause cannot see let declarations that appear inside the loop. So we compromise and use var, so that done is hoisted to the outer scope where it can be seen.

The alternative—declaring done outside the loop—separates it from where it’s first used, and either necessitates picking a default value to assign, or worse, leaving it unassigned and thus looking ambiguous to the reader. I think var inside the loop is preferable here.

Another helpful characteristic of var is seen with declarations inside unintended blocks. Unintended blocks are blocks that are created because the syntax requires a block, but where the intent of the developer is not really to create a localized scope. The best illustration of unintended scope is the try..catch statement:

There are other ways to structure this code, yes. But I think this is the best way, given various trade-offs.

I don’t want to declare records (with var or let) outside of the try block, and then assign to it in one or both blocks. I prefer initial declarations to always be as close as possible (ideally, same line) to the first usage of the variable. In this simple example, that would only be a couple of lines distance, but in real code it can grow to many more lines. The bigger the gap, the harder it is to figure out what variable from what scope you’re assigning to. var used at the actual assignment makes it less ambiguous.

Also notice I used var in both the try and catch blocks. That’s because I want to signal to the reader that no matter which path is taken, records always gets declared. Technically, that works because var is hoisted once to the function scope. But it’s still a nice semantic signal to remind the reader what either var ensures. If var were only used in one of the blocks, and you were only reading the other block, you wouldn’t as easily discover where records was coming from.

This is, in my opinion, a little superpower of var. Not only can it escape the unintentional try..catch blocks, but it’s allowed to appear multiple times in a function’s scope. You can’t do that with let. It’s not bad, it’s actually a little helpful feature. Think of var more like a declarative annotation that’s reminding you, each usage, where the variable comes from. “Ah ha, right, it belongs to the whole function.”

This repeated-annotation superpower is useful in other cases:

The second var data is not re-declaring data, it’s just annotating for the readers’ benefit that data is a function-wide declaration. That way, the reader doesn’t need to scroll up 50+ lines of code to find the initial declaration.

I’m perfectly fine with re-using variables for multiple purposes throughout a function scope. I’m also perfectly fine with having two usages of a variable be separated by quite a few lines of code. In both cases, the ability to safely “re-declare” (annotate) with var helps make sure I can tell where my data is coming from, no matter where I am in the function.

Again, sadly, let cannot do this.

There are other nuances and scenarios when var turns out to offer some assistance, but I’m not going to belabor the point any further. The takeaway is that var can be useful in our programs alongside let (and the occasional const). Are you willing to creatively use the tools the JS language provides to tell a richer story to your readers?

Don’t just throw away a useful tool like var because someone shamed you into thinking it wasn’t cool anymore. Don’t avoid var because you got confused once years ago. Learn these tools and use them each for what they’re best at.
