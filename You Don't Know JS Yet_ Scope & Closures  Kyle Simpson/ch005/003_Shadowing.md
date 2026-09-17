# ch005

## Shadowing


“Shadowing” might sound mysterious and a little bit sketchy. But don’t worry, it’s completely legit!

Our running example for these chapters uses different variable names across the scope boundaries. Since they all have unique names, in a way it wouldn’t matter if all of them were just stored in one bucket (like RED(1)).

Where having different lexical scope buckets starts to matter more is when you have two or more variables, each in different scopes, with the same lexical names. A single scope cannot have two or more variables with the same name; such multiple references would be assumed as just one variable.

So if you need to maintain two or more variables of the same name, you must use separate (often nested) scopes. And in that case, it’s very relevant how the different scope buckets are laid out.

The studentName variable on line 1 (the var studentName = .. statement) creates a RED(1) marble. The same named variable is declared as a BLUE(2) marble on line 3, the parameter in the printStudent(..) function definition.

What color marble will studentName be in the studentName = studentName.toUpperCase() assignment statement and the console.log(studentName) statement? All three studentName references will be BLUE(2).

With the conceptual notion of the “lookup,” we asserted that it starts with the current scope and works its way outward/upward, stopping as soon as a matching variable is found. The BLUE(2) studentName is found right away. The RED(1) studentName is never even considered.

This is a key aspect of lexical scope behavior, called shadowing. The BLUE(2) studentName variable (parameter) shadows the RED(1) studentName. So, the parameter is shadowing the (shadowed) global variable. Repeat that sentence to yourself a few times to make sure you have the terminology straight!

That’s why the re-assignment of studentName affects only the inner (parameter) variable: the BLUE(2) studentName, not the global RED(1) studentName.

When you choose to shadow a variable from an outer scope, one direct impact is that from that scope inward/downward (through any nested scopes) it’s now impossible for any marble to be colored as the shadowed variable—(RED(1), in this case). In other words, any studentName identifier reference will correspond to that parameter variable, never the global studentName variable. It’s lexically impossible to reference the global studentName anywhere inside of the printStudent(..) function (or from any nested scopes).
