# ch004

## Building On Metaphors


To visualize nested scope resolution, I prefer yet another metaphor, an office building, as in Figure 3:

The building represents our program’s nested scope collection. The first floor of the building represents the currently executing scope. The top level of the building is the global scope.

You resolve a target or source variable reference by first looking on the current floor, and if you don’t find it, taking the elevator to the next floor (i.e., an outer scope), looking there, then the next, and so on. Once you get to the top floor (the global scope), you either find what you’re looking for, or you don’t. But you have to stop regardless.
