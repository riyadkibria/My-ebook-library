# ch012

## Modules


This exercise is to convert the calculator from Closure (PART 3) into a module.

We’re not adding any additional functionality to the calculator, only changing its interface. Instead of calling a single function calc(..), we’ll be calling specific methods on the public API for each “keypress” of our calculator. The outputs stay the same.

This module should be expressed as a classic module factory function called calculator(), instead of a singleton IIFE, so that multiple calculators can be created if desired.

The public API should include the following methods:

Usage would look like:

formatTotal(..) remains the same from that previous exercise. But the useCalc(..) helper needs to be adjusted to work with the module API:

Try the exercise for yourself, then check out the suggested solution at the end of this appendix.

As you work on this exercise, also spend some time considering the pros/cons of representing the calculator as a module as opposed to the closure-function approach from the previous exercise.

BONUS: write out a few sentences explaining your thoughts.

BONUS #2: try converting your module to other module formats, including: UMD, CommonJS, and ESM (ES Modules).
