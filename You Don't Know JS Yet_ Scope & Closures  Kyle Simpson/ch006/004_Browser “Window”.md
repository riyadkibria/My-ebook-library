# ch006

## Browser “Window”


With respect to treatment of the global scope, the most pure environment JS can be run in is as a standalone .js file loaded in a web page environment in a browser. I don’t mean “pure” as in nothing automatically added—lots may be added!—but rather in terms of minimal intrusion on the code or interference with its expected global scope behavior.

Consider this .js file:

This code may be loaded in a web page environment using an inline <script> tag, a <script src=..> script tag in the markup, or even a dynamically created <script> DOM element. In all three cases, the studentName and hello identifiers are declared in the global scope.

That means if you access the global object (commonly, window in the browser), you’ll find properties of those same names there:

That’s the default behavior one would expect from a reading of the JS specification: the outer scope is the global scope and studentName is legitimately created as global variable.

That’s what I mean by pure. But unfortunately, that won’t always be true of all JS environments you encounter, and that’s often surprising to JS developers.
