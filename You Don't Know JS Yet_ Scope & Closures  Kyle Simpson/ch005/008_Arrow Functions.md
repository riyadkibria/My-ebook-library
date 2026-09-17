# ch005

## Arrow Functions


ES6 added an additional function expression form to the language, called “arrow functions”:

The => arrow function doesn’t require the word function to define it. Also, the ( .. ) around the parameter list is optional in some simple cases. Likewise, the { .. } around the function body is optional in some cases. And when the { .. } are omitted, a return value is sent out without using a return keyword.

Arrow functions are lexically anonymous, meaning they have no directly related identifier that references the function. The assignment to askQuestion creates an inferred name of “askQuestion”, but that’s not the same thing as being non-anonymous:

Arrow functions achieve their syntactic brevity at the expense of having to mentally juggle a bunch of variations for different forms/conditions. Just a few, for example:

The real reason I bring up arrow functions is because of the common but incorrect claim that arrow functions somehow behave differently with respect to lexical scope from standard function functions.

Other than being anonymous (and having no declarative form), => arrow functions have the same lexical scope rules as function functions do. An arrow function, with or without { .. } around its body, still creates a separate, inner nested bucket of scope. Variable declarations inside this nested scope bucket behave the same as in a function scope.
