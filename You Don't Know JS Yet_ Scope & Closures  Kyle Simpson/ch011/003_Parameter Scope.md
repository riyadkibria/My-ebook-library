# ch011

## Parameter Scope


The conversation metaphor in Chapter 2 implies that function parameters are basically the same as locally declared variables in the function scope. But that’s not always true.

Here, studentID is a considered a “simple” parameter, so it does behave as a member of the BLUE(2) function scope. But if we change it to be a non-simple parameter, that’s no longer technically the case. Parameter forms considered non-simple include parameters with default values, rest parameters (using ...), and destructured parameters.

Here, the parameter list essentially becomes its own scope, and the function’s scope is then nested inside that scope.

Why? What difference does it make? The non-simple parameter forms introduce various corner cases, so the parameter list becomes its own scope to more effectively deal with them.

Assuming left-to-right operations, the default = maxID for the studentID parameter requires a maxID to already exist (and to have been initialized). This code produces a TDZ error (Chapter 5). The reason is that maxID is declared in the parameter scope, but it’s not yet been initialized because of the order of parameters. If the parameter order is flipped, no TDZ error occurs:

The complication gets even more in the weeds if we introduce a function expression into the default parameter position, which then can create its own closure (Chapter 7) over parameters in this implied parameter scope:

That snippet probably makes sense, because the defaultID() arrow function closes over the id parameter/variable, which we then re-assign to 5. But now let’s introduce a shadowing definition of id in the function scope:

Uh oh! The var id = 5 is shadowing the id parameter, but the closure of the defaultID() function is over the parameter, not the shadowing variable in the function body. This proves there’s a scope bubble around the parameter list.

But it gets even crazier than that!

The strange bit here is the first console message. At that moment, the shadowing id local variable has just been var id declared, which Chapter 5 asserts is typically auto-initialized to undefined at the top of its scope. Why doesn’t it print undefined?

In this specific corner case (for legacy compat reasons), JS doesn’t auto-initialize id to undefined, but rather to the value of the id parameter (3)!

Though the two ids look at that moment like they’re one variable, they’re actually still separate (and in separate scopes). The id = 5 assignment makes the divergence observable, where the id parameter stays 3 and the local variable becomes 5.

My advice to avoid getting bitten by these weird nuances:

Never shadow parameters with local variables

Avoid using a default parameter function that closes over any of the parameters

At least now you’re aware and can be careful about the fact that the parameter list is its own scope if any of the parameters are non-simple.
