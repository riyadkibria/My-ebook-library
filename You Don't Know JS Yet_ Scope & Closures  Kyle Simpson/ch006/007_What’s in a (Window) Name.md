# ch006

## What’s in a (Window) Name?


Another global scope oddity in browser-based JS:

window.name is a pre-defined “global” in a browser context; it’s a property on the global object, so it seems like a normal global variable (yet it’s anything but “normal”).

We used var for our declaration, which does not shadow the pre-defined name global property. That means, effectively, the var declaration is ignored, since there’s already a global scope object property of that name. As we discussed earlier, had we used let name, we would have shadowed window.name with a separate global name variable.

But the truly surprising behavior is that even though we assigned the number 42 to name (and thus window.name), when we then retrieve its value, it’s a string "42"! In this case, the weirdness is because name is actually a pre-defined getter/setter on the window object, which insists on its value being a string value. Yikes!

With the exception of some rare corner cases like DOM element ID’s and window.name, JS running as a standalone file in a browser page has some of the most pure global scope behavior we will encounter.
