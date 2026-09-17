# ch004

## Lookup Failures


When Engine exhausts all lexically available scopes (moving outward) and still cannot resolve the lookup of an identifier, an error condition then exists. However, depending on the mode of the program (strict-mode or not) and the role of the variable (i.e., target vs. source; see Chapter 1), this error condition will be handled differently.
