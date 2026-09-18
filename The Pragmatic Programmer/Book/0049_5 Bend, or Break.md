# 5 Bend, or Break


**Source File:**

None


**Word Count:**

None



---

Chapter 5

Bend, or Break

Life doesn’t stand still. Neither can the code that we write. In order to keep up with today’s near-frantic pace of change, we need to make every effort to write code that’s as loose—as flexible—as possible. Otherwise we may find our code quickly becoming outdated, or too brittle to fix, and may ultimately be left behind in the mad dash toward the future.

Back in Topic 11, ​ Reversibility ​ we talked about the perils of irreversible decisions. In this chapter, we’ll tell you how to make reversible decisions, so your code can stay flexible and adaptable in the face of an uncertain world.

reversible

First we look at coupling —the dependencies between bits of code. Topic 28, ​ Decoupling ​ shows how to keep separate concepts separate, decreasing coupling.

coupling

Next, we’ll look at different techniques you can use when Topic 29, ​ Juggling the Real World ​ . We’ll examine four different strategies to help manage and react to events—a critical aspect of modern software applications.

Traditional procedural and object-oriented code might be too tightly coupled for your purposes. In Topic 30, ​ Transforming Programming ​ , we’ll take advantage of the more flexible and clearer style offered by function pipelines, even if your language doesn’t support them directly.

Common object-oriented style can tempt you with another trap. Don’t fall for it, or you’ll end up paying a hefty Topic 31, ​ Inheritance Tax ​ . We’ll explore better alternatives to keep your code flexible and easier to change.

And of course a good way to stay flexible is to write less code. Changing code leaves you open to the possibility of introducing new bugs. Topic 32, ​ Configuration ​ will explain how to move details out of the code completely, where they can be changed more safely and easily.

less

All these techniques will help you write code that bends and doesn’t break.

