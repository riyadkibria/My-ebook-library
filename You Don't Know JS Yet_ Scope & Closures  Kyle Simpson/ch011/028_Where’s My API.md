# ch011

## Where’s My API?


First, most classic modules don’t define and use a publicAPI the way I have shown in this code. Instead, they typically look like:

The only difference here is directly returning the object that serves as the public API for the module, as opposed to first saving it to an inner publicAPI variable. This is by far how most classic modules are defined.

But I strongly prefer, and always use myself, the former publicAPI form. Two reasons:

publicAPI is a semantic descriptor that aids readability by making it more obvious what the purpose of the object is.

Storing an inner publicAPI variable that references the same external public API object returned, can be useful if you need to access or modify the API during the lifetime of the module.

For example, you may want to call one of the publicly exposed functions, from inside the module. Or, you may want to add or remove methods depending on certain conditions, or update the value of an exposed property.

Whatever the case may be, it just seems rather silly to me that we wouldn’t maintain a reference to access our own API. Right?
