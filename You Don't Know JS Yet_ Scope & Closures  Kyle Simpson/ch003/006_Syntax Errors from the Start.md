# ch003

## Syntax Errors from the Start


Consider this program:

This program produces no output ("Hello" is not printed), but instead throws a SyntaxError about the unexpected . token right before the "Hi" string. Since the syntax error happens after the well-formed console.log(..) statement, if JS was executing top-down line by line, one would expect the "Hello" message being printed before the syntax error being thrown. That doesn’t happen.

In fact, the only way the JS engine could know about the syntax error on the third line, before executing the first and second lines, is by the JS engine first parsing the entire program before any of it is executed.
