# Looking for Concurrency


**Source File:**

None


**Word Count:**

None



---

Topic 33

Topic 33

“What is temporal coupling all about?”, you may ask. It’s about time.

temporal coupling

Time is an often ignored aspect of software architectures. The only time that preoccupies us is the time on the schedule, the time left until we ship—but this is not what we’re talking about here. Instead, we are talking about the role of time as a design element of the software itself. There are two aspects of time that are important to us: concurrency (things happening at the same time) and ordering (the relative positions of things in time).

We don’t usually approach programming with either of these aspects in mind. When people first sit down to design an architecture or write a program, things tend to be linear. That’s the way most people think— do this and then always do that . But thinking this way leads to temporal coupling : coupling in time. Method A must always be called before method B ; only one report can be run at a time; you must wait for the screen to redraw before the button click is received. Tick must happen before tock.

do this

do that

temporal coupling

This approach is not very flexible, and not very realistic.

We need to allow for concurrency and to think about decoupling any time or order dependencies. In doing so, we can gain flexibility and reduce any time-based dependencies in many areas of development: workflow analysis, architecture, design, and deployment. The result will be systems that are easier to reason about, that potentially respond faster and more reliably.

On many projects, we need to model and analyze the application workflows as part of the design. We’d like to find out what can happen at the same time, and what must happen in a strict order. One way to do this is to capture the workflow using a notation such as the activity diagram . [46]

can

must

activity diagram

An activity diagram consists of a set of actions drawn as rounded boxes. The arrow leaving an action leads to either another action (which can start once the first action completes) or to a thick line called a synchronization bar . Once all the actions leading into a synchronization bar are complete, you can then proceed along any arrows leaving the bar. An action with no arrows leading into it can be started at any time.

synchronization bar

all

You can use activity diagrams to maximize parallelism by identifying activities that could be performed in parallel, but aren’t.

could be

For instance, we may be writing the software for a robotic piña colada maker. We’re told that the steps are:

Open blender

Open piña colada mix

Put mix in blender

Measure 1/2 cup white rum

Pour in rum

Add 2 cups of ice

Close blender

Liquefy for 1 minute

Open blender

Get glasses

Get pink umbrellas

Serve

However, a bartender would lose their job if they followed these steps, one by one, in order. Even though they describe these actions serially, many of them could be performed in parallel. We’ll use the following activity diagram to capture and reason about potential concurrency.

It can be eye-opening to see where the dependencies really exist. In this instance, the top-level tasks (1, 2, 4, 10, and 11) can all happen concurrently, up front. Tasks 3, 5, and 6 can happen in parallel later. If you were in a piña colada-making contest, these optimizations may make all the difference.

Faster Formatting This book is written in plain text. To build the version to be printed, or an ebook, or whatever, that text is fed through a pipeline of processors. Some look for particular constructs (bibliography citations, index entries, special markup for tips, and so on). Other processors operate on the document as a whole. Many of the processors in the pipeline have to access external information (reading files, writing files, piping through external programs). All this relatively slow speed work gives us the opportunity to exploit concurrency: in fact each step in the pipeline executes concurrently, reading from the previous step and writing to the next. In addition, some parts of the process are relatively processor intensive. One of these is the conversion of mathematical formulae. For various historical reasons each equation can take up to 500ms to convert. To speed things up, we take advantage of parallelism. Because each formula is independent of the others, we convert each in its own parallel process and collect the results back into the book as they become available. As a result, the book builds much, much faster on multicore machines. (And, yes, we did indeed discover a number of concurrency errors in our pipeline along the way….)

Faster Formatting

This book is written in plain text. To build the version to be printed, or an ebook, or whatever, that text is fed through a pipeline of processors. Some look for particular constructs (bibliography citations, index entries, special markup for tips, and so on). Other processors operate on the document as a whole. Many of the processors in the pipeline have to access external information (reading files, writing files, piping through external programs). All this relatively slow speed work gives us the opportunity to exploit concurrency: in fact each step in the pipeline executes concurrently, reading from the previous step and writing to the next. In addition, some parts of the process are relatively processor intensive. One of these is the conversion of mathematical formulae. For various historical reasons each equation can take up to 500ms to convert. To speed things up, we take advantage of parallelism. Because each formula is independent of the others, we convert each in its own parallel process and collect the results back into the book as they become available. As a result, the book builds much, much faster on multicore machines. (And, yes, we did indeed discover a number of concurrency errors in our pipeline along the way….)

This book is written in plain text. To build the version to be printed, or an ebook, or whatever, that text is fed through a pipeline of processors. Some look for particular constructs (bibliography citations, index entries, special markup for tips, and so on). Other processors operate on the document as a whole.

Many of the processors in the pipeline have to access external information (reading files, writing files, piping through external programs). All this relatively slow speed work gives us the opportunity to exploit concurrency: in fact each step in the pipeline executes concurrently, reading from the previous step and writing to the next.

In addition, some parts of the process are relatively processor intensive. One of these is the conversion of mathematical formulae. For various historical reasons each equation can take up to 500ms to convert. To speed things up, we take advantage of parallelism. Because each formula is independent of the others, we convert each in its own parallel process and collect the results back into the book as they become available.

As a result, the book builds much, much faster on multicore machines.

(And, yes, we did indeed discover a number of concurrency errors in our pipeline along the way….)

Activity diagrams show the potential areas of concurrency, but have nothing to say about whether these areas are worth exploiting. For example, in the piña colada example, a bartender would need five hands to be able to run all the potential initial tasks at once.

And that’s where the design part comes in. When we look at the activities, we realize that number 8, liquify, will take a minute. During that time, our bartender can get the glasses and umbrellas (activities 10 and 11) and probably still have time to serve another customer.

And that’s what we’re looking for when we’re designing for concurrency. We’re hoping to find activities that take time, but not time in our code. Querying a database, accessing an external service, waiting for user input: all these things would normally stall our program until they complete. And these are all opportunities to do something more productive than the CPU equivalent of twiddling one’s thumbs.

Remember the distinction: concurrency is a software mechanism, and parallelism is a hardware concern. If we have multiple processors, either locally or remotely, then if we can split work out among them we can reduce the overall time things take.

The ideal things to split this way are pieces of work that are relatively independent—where each can proceed without waiting for anything from the others. A common pattern is to take a large piece of work, split it into independent chunks, process each in parallel, then combine the results.

An interesting example of this in practice is the way the compiler for the Elixir language works. When it starts, it splits the project it is building into modules, and compiles each in parallel. Sometimes a module depends on another, in which case its compilation pauses until the results of the other module’s build become available. When the top-level module completes, it means that all dependencies have been compiled. The result is a speedy compilation that takes advantage of all the cores available.

Back to your applications. We’ve identified places where it will benefit from concurrency and parallelism. Now for the tricky part: how can we implement it safely. That’s the topic of the rest of the chapter.

Topic 10, ​ Orthogonality ​

Topic 26, ​ How to Balance Resources ​

Topic 28, ​ Decoupling ​

Topic 36, ​ Blackboards ​

How many tasks do you perform in parallel when you get ready for work in the morning? Could you express this in a UML activity diagram? Can you find some way to get ready more quickly by increasing concurrency?

