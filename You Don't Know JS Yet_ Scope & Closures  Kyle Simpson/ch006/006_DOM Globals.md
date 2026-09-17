# ch006

## DOM Globals


I asserted that a browser-hosted JS environment has the most pure global scope behavior we’ll see. However, it’s not entirely pure.

One surprising behavior in the global scope you may encounter with browser-based JS applications: a DOM element with an id attribute automatically creates a global variable that references it.

Consider this markup:

And the JS for that page could include:

If the id value is a valid lexical name (like first), the lexical variable is created. If not, the only way to access that global is through the global object (window[..]).

The auto-registration of all id-bearing DOM elements as global variables is an old legacy browser behavior that nevertheless must remain because so many old sites still rely on it. My advice is never to use these global variables, even though they will always be silently created.
