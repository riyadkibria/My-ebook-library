# ch006

## Globals Shadowing Globals


Recall the discussion of shadowing (and global unshadowing) from Chapter 3, where one variable declaration can override and prevent access to a declaration of the same name from an outer scope.

An unusual consequence of the difference between a global variable and a global property of the same name is that, within just the global scope itself, a global object property can be shadowed by a global variable:

The let declaration adds a something global variable but not a global object property (see Chapter 3). The effect then is that the something lexical identifier shadows the something global object property.

It’s almost certainly a bad idea to create a divergence between the global object and the global scope. Readers of your code will almost certainly be tripped up.

A simple way to avoid this gotcha with global declarations: always use var for globals. Reserve let and const for block scopes (see “Scoping with Blocks” in Chapter 6).
