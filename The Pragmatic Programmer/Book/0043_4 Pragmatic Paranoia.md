# 4 Pragmatic Paranoia


**Source File:**

None


**Word Count:**

None



---

Chapter 4

Pragmatic Paranoia

Did that hurt? It shouldn’t. Accept it as an axiom of life. Embrace it. Celebrate it. Because perfect software doesn’t exist. No one in the brief history of computing has ever written a piece of perfect software. It’s unlikely that you’ll be the first. And unless you accept this as a fact, you’ll end up wasting time and energy chasing an impossible dream.

So, given this depressing reality, how does a Pragmatic Programmer turn it into an advantage? That’s the topic of this chapter.

Everyone knows that they personally are the only good driver on Earth. The rest of the world is out there to get them, blowing through stop signs, weaving between lanes, not indicating turns, texting on the phone, and just generally not living up to our standards. So we drive defensively. We look out for trouble before it happens, anticipate the unexpected, and never put ourselves into a position from which we can’t extricate ourselves.

The analogy with coding is pretty obvious. We are constantly interfacing with other people’s code—code that might not live up to our high standards—and dealing with inputs that may or may not be valid. So we are taught to code defensively. If there’s any doubt, we validate all information we’re given. We use assertions to detect bad data, and distrust data from potential attackers or trolls. We check for consistency, put constraints on database columns, and generally feel pretty good about ourselves.

But Pragmatic Programmers take this a step further. They don’t trust themselves, either. Knowing that no one writes perfect code, including themselves, Pragmatic Programmers build in defenses against their own mistakes. We describe the first defensive measure in Topic 23, ​ Design by Contract ​ : clients and suppliers must agree on rights and responsibilities.

They don’t trust themselves, either.

In Topic 24, ​ Dead Programs Tell No Lies ​ , we want to ensure that we do no damage while we’re working the bugs out. So we try to check things often and terminate the program if things go awry.

Topic 25, ​ Assertive Programming ​ describes an easy method of checking along the way—write code that actively verifies your assumptions.

As your programs get more dynamic, you’ll find yourself juggling system resources—memory, files, devices, and the like. In Topic 26, ​ How to Balance Resources ​ , we’ll suggest ways of ensuring that you don’t drop any of the balls.

And most importantly, we stick to small steps always, as described in Topic 27, ​ Don’t Outrun Your Headlights ​ , so we don’t fall off the edge of the cliff.

In a world of imperfect systems, ridiculous time scales, laughable tools, and impossible requirements, let’s play it safe. As Woody Allen said, “When everybody actually is out to get you, paranoia is just good thinking.”

