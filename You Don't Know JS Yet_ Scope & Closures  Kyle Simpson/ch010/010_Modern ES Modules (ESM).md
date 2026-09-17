# ch010

## Modern ES Modules (ESM)


The ESM format shares several similarities with the CommonJS format. ESM is file-based, and module instances are singletons, with everything private by default. One notable difference is that ESM files are assumed to be strict-mode, without needing a "use strict" pragma at the top. There’s no way to define an ESM as non-strict-mode.

Instead of module.exports in CommonJS, ESM uses an export keyword to expose something on the public API of the module. The import keyword replaces the require(..) statement. Let’s adjust “students.js” to use the ESM format:

The only change here is the export { getName } statement. As before, export statements can appear anywhere throughout the file, though export must be at the top-level scope; it cannot be inside any other block or function.

ESM offers a fair bit of variation on how the export statements can be specified. For example:

Even though export appears before the function keyword here, this form is still a function declaration that also happens to be exported. That is, the getName identifier is function hoisted (see Chapter 5), so it’s available throughout the whole scope of the module.

Another allowed variation:

This is a so-called “default export,” which has different semantics from other exports. In essence, a “default export” is a shorthand for consumers of the module when they import, giving them a terser syntax when they only need this single default API member.

Non-default exports are referred to as “named exports.”

The import keyword—like export, it must be used only at the top level of an ESM outside of any blocks or functions—also has a number of variations in syntax. The first is referred to as “named import”:

As you can see, this form imports only the specifically named public API members from a module (skipping anything not named explicitly), and it adds those identifiers to the top-level scope of the current module. This type of import is a familiar style to those used to package imports in languages like Java.

Multiple API members can be listed inside the { .. } set, separated with commas. A named import can also be renamed with the as keyword:

If getName is a “default export” of the module, we can import it like this:

The only difference here is dropping the { } around the import binding. If you want to mix a default import with other named imports:

By contrast, the other major variation on import is called “namespace import”:

As is likely obvious, the * imports everything exported to the API, default and named, and stores it all under the single namespace identifier as specified. This approach most closely matches the form of classic modules for most of JS’s history.
