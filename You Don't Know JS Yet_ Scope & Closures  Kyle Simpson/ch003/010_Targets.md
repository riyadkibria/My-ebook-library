# ch003

## Targets


What makes a variable a target? Consider:

This statement is clearly an assignment operation; remember, the var students part is handled entirely as a declaration at compile time, and is thus irrelevant during execution; we left it out for clarity and focus. Same with the nextStudent = getStudentName(73) statement.

But there are three other target assignment operations in the code that are perhaps less obvious. One of them:

That statement assigns a value to student for each iteration of the loop. Another target reference:

But how is that an assignment to a target? Look closely: the argument 73 is assigned to the parameter studentID.

And there’s one last (subtle) target reference in our program. Can you spot it?

Did you identify this one?

A function declaration is a special case of a target reference. You can think of it sort of like var getStudentName = function(studentID), but that’s not exactly accurate. An identifier getStudentName is declared (at compile time), but the = function(studentID) part is also handled at compilation; the association between getStudentName and the function is automatically set up at the beginning of the scope rather than waiting for an = assignment statement to be executed.
