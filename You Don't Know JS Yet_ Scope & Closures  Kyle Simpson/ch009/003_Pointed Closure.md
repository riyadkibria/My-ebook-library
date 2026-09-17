# ch009

## Pointed Closure


Actually, we glossed over a little detail in the previous discussion which I’m guessing many readers missed!

Because of how terse the syntax for => arrow functions is, it’s easy to forget that they still create a scope (as asserted in “Arrow Functions” in Chapter 3). The student => student.id == studentID arrow function is creating another scope bubble inside the greetStudent(..) function scope.

Building on the metaphor of colored buckets and bubbles from Chapter 2, if we were creating a colored diagram for this code, there’s a fourth scope at this innermost nesting level, so we’d need a fourth color; perhaps we’d pick ORANGE(4) for that scope:

The BLUE(2) studentID reference is actually inside the ORANGE(4) scope rather than the GREEN(3) scope of greetStudent(..); also, the student parameter of the arrow function is ORANGE(4), shadowing the GREEN(3) student.

The consequence here is that this arrow function passed as a callback to the array’s find(..) method has to hold the closure over studentID, rather than greetStudent(..) holding that closure. That’s not too big of a deal, as everything still works as expected. It’s just important not to skip over the fact that even tiny arrow functions can get in on the closure party.
