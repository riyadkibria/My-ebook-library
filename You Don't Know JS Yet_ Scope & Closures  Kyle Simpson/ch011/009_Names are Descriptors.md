# ch011

## Names are Descriptors


Lastly, and I think most importantly of all, leaving off a name from a function makes it harder for the reader to tell what the function’s purpose is, at a quick glance. They have to read more of the code, including the code inside the function, and the surrounding code outside the function, to figure it out.

There’s just no reasonable argument to be made that omitting the name keepOnlyOdds from the first callback more effectively communicates to the reader the purpose of this callback. You saved 13 characters, but lost important readability information. The name keepOnlyOdds very clearly tells the reader, at a quick first glance, what’s happening.

The JS engine doesn’t care about the name. But human readers of your code absolutely do.

Can the reader look at v % 2 == 1 and figure out what it’s doing? Sure. But they have to infer the purpose (and name) by mentally executing the code. Even a brief pause to do so slows down reading of the code. A good descriptive name makes this process almost effortless and instant.

Think of it this way: how many times does the author of this code need to figure out the purpose of a function before adding the name to the code? About once. Maybe two or three times if they need to adjust the name. But how many times will readers of this code have to figure out the name/purpose? Every single time this line is ever read. Hundreds of times? Thousands? More?

No matter the length or complexity of the function, my assertion is, the author should figure out a good descriptive name and add it to the code. Even the one-liner functions in map(..) and then(..) statements should be named:

The name extractSalesRecords tells the reader the purpose of this then(..) handler better than just inferring that purpose from mentally executing return resp.allSales.

The only excuse for not including a name on a function is either laziness (don’t want to type a few extra characters) or uncreativity (can’t come up with a good name). If you can’t figure out a good name, you likely don’t understand the function and its purpose yet. The function is perhaps poorly designed, or it does too many things, and should be re-worked. Once you have a well-designed, single-purpose function, its proper name should become evident.

Here’s a trick I use: while first writing a function, if I don’t fully understand its purpose and can’t think of a good name to use, I just use TODO as the name. That way, later when reviewing my code, I’m likely to find those name placeholders, and I’m more inclined (and more prepared!) to go back and figure out a better name, rather than just leave it as TODO.

All functions need names. Every single one. No exceptions. Any name you omit is making the program harder to read, harder to debug, harder to extend and maintain later.
