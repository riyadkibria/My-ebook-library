# ch011

## Universal Modules (UMD)


The final variation we’ll look at is UMD, which is less a specific, exact format and more a collection of very similar formats. It was designed to create better interop (without any build-tool conversion) for modules that may be loaded in browsers, by AMD-style loaders, or in Node. I personally still publish many of my utility libraries using a form of UMD.

Here’s the typical structure of a UMD:

Though it may look a bit unusual, UMD is really just an IIFE.

What’s different is that the main function expression part (at the top) of the IIFE contains a series of if..else if statements to detect which of the three supported environments the module is being loaded in.

The final () that normally invokes an IIFE is being passed three arguments: "StudentsList", this, and another function expression. If you match those arguments to their parameters, you’ll see they are: name, context, and definition, respectively. "StudentList" (name) is the name label for the module, primarily in case it’s defined as a global variable. this (context) is generally the window (aka, global object; see Chapter 4) for defining the module by its name.

definition(..) is invoked to actually retrieve the definition of the module, and you’ll notice that, sure enough, that’s just a classic module form!

There’s no question that as of the time of this writing, ESM (ES Modules) are becoming popular and widespread rapidly. But with millions and millions of modules written over the last 20 years, all using some pre-ESM variation of classic modules, they’re still very important to be able to read and understand when you come across them.

Inversion of Control, Martin Fowler, https://martinfowler.com/bliki/InversionOfControl.html, 26 June 2005.↩︎
