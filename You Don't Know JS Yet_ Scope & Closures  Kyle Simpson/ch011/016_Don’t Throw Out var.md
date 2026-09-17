# ch011

## Don’t Throw Out var


var is fine, and works just fine. It’s been around for 25 years, and it’ll be around and useful and functional for another 25 years or more. Claims that var is broken, deprecated, outdated, dangerous, or ill-designed are bogus bandwagoning.

Does that mean var is the right declarator for every single declaration in your program? Certainly not. But it still has its place in your programs. Refusing to use it because someone on the team chose an aggressive linter opinion that chokes on var is cutting off your nose to spite your face.

OK, now that I’ve got you really riled up, let me try to explain my position.

For the record, I’m a fan of let, for block-scoped declarations. I really dislike TDZ and I think that was a mistake. But let itself is great. I use it often. In fact, I probably use it as much or more than I use var.
