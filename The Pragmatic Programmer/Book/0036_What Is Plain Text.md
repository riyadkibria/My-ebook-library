# What Is Plain Text


**Source File:**

None


**Word Count:**

None



---

Topic 16

Topic 16

As Pragmatic Programmers, our base material isn’t wood or iron, it’s knowledge. We gather requirements as knowledge, and then express that knowledge in our designs, implementations, tests, and documents. And we believe that the best format for storing knowledge persistently is plain text . With plain text, we give ourselves the ability to manipulate knowledge, both manually and programmatically, using virtually every tool at our disposal.

plain text

The problem with most binary formats is that the context necessary to understand the data is separate from the data itself. You are artificially divorcing the data from its meaning. The data may as well be encrypted; it is absolutely meaningless without the application logic to parse it. With plain text, however, you can achieve a self-describing data stream that is independent of the application that created it.

Plain text is made up of printable characters in a form that conveys information. It can be as simple as a shopping list:

Plain text

or as complex as the source of this book (yes, it’s in plain text, much to the chagrin of the publisher, who wanted us to use a word processor).

The information part is important. The following is not useful plain text:

Neither is this:

The reader has no idea what the significance of 467abe may be. We like our plain text to be understandable to humans.

467abe

understandable

Plain text doesn’t mean that the text is unstructured; HTML, JSON, YAML, and so on are all plain text. So are the majority of the fundamental protocols on the net, such as HTTP, SMTP, IMAP, and so on. And that’s for some good reasons:

Insurance against obsolescence

Leverage existing tools

Easier testing

Human-readable forms of data, and self-describing data, will outlive all other forms of data and the applications that created them. Period. As long as the data survives, you will have a chance to be able to use it—potentially long after the original application that wrote it is defunct.

You can parse such a file with only partial knowledge of its format; with most binary files, you must know all the details of the entire format in order to parse it successfully.

Consider a data file from some legacy system that you are given. [24] You know little about the original application; all that’s important to you is that it maintained a list of clients’ Social Security numbers, which you need to find and extract. Among the data, you see

Recognizing the format of a Social Security number, you can quickly write a small program to extract that data—even if you have no information on anything else in the file.

But imagine if the file had been formatted this way instead:

You may not have recognized the significance of the numbers quite as easily. This is the difference between human readable and human understandable .

human readable

human understandable

While we’re at it, FIELD10 doesn’t help much either. Something like

FIELD10

makes the exercise a no-brainer—and ensures that the data will outlive any project that created it.

Virtually every tool in the computing universe, from version control systems to editors to command-line tools, can operate on plain text.

The Unix Philosophy Unix is famous for being designed around the philosophy of small, sharp tools, each intended to do one thing well. This philosophy is enabled by using a common underlying format—the line-oriented, plain-text file. Databases used for system administration (users and passwords, networking configuration, and so on) are all kept as plain-text files. (Some systems also maintain a binary form of certain databases as a performance optimization. The plain-text version is kept as an interface to the binary version.) When a system crashes, you may be faced with only a minimal environment to restore it (you may not be able to access graphics drivers, for instance). Situations such as this can really make you appreciate the simplicity of plain text. Plain text is also easier to search. If you can’t remember which configuration file manages your system backups, a quick grep -r backup /etc should tell you.

The Unix Philosophy

Unix is famous for being designed around the philosophy of small, sharp tools, each intended to do one thing well. This philosophy is enabled by using a common underlying format—the line-oriented, plain-text file. Databases used for system administration (users and passwords, networking configuration, and so on) are all kept as plain-text files. (Some systems also maintain a binary form of certain databases as a performance optimization. The plain-text version is kept as an interface to the binary version.) When a system crashes, you may be faced with only a minimal environment to restore it (you may not be able to access graphics drivers, for instance). Situations such as this can really make you appreciate the simplicity of plain text. Plain text is also easier to search. If you can’t remember which configuration file manages your system backups, a quick grep -r backup /etc should tell you.

Unix is famous for being designed around the philosophy of small, sharp tools, each intended to do one thing well. This philosophy is enabled by using a common underlying format—the line-oriented, plain-text file. Databases used for system administration (users and passwords, networking configuration, and so on) are all kept as plain-text files. (Some systems also maintain a binary form of certain databases as a performance optimization. The plain-text version is kept as an interface to the binary version.)

When a system crashes, you may be faced with only a minimal environment to restore it (you may not be able to access graphics drivers, for instance). Situations such as this can really make you appreciate the simplicity of plain text.

Plain text is also easier to search. If you can’t remember which configuration file manages your system backups, a quick grep -r backup /etc should tell you.

grep -r backup /etc

For instance, suppose you have a production deployment of a large application with a complex site-specific configuration file. If this file is in plain text, you could place it under a version control system (see Topic 19, ​ Version Control ​ ), so that you automatically keep a history of all changes. File comparison tools such as diff and fc allow you to see at a glance what changes have been made, while sum allows you to generate a checksum to monitor the file for accidental (or malicious) modification.

diff

sum

If you use plain text to create synthetic data to drive system tests, then it is a simple matter to add, update, or modify the test data without having to create any special tools to do so. Similarly, plain-text output from regression tests can be trivially analyzed with shell commands or a simple script.

without having to create any special tools to do so.

Even in the future of blockchain-based intelligent agents that travel the wild and dangerous internet autonomously, negotiating data interchange among themselves, the ubiquitous text file will still be there. In fact, in heterogeneous environments the advantages of plain text can outweigh all of the drawbacks. You need to ensure that all parties can communicate using a common standard. Plain text is that standard.

Topic 17, ​ Shell Games ​

Topic 21, ​ Text Manipulation ​

Topic 32, ​ Configuration ​

Design a small address book database (name, phone number, and so on) using a straightforward binary representation in your language of choice. Do this before reading the rest of this challenge. Translate that format into a plain-text format using XML or JSON. For each version, add a new, variable-length field called directions in which you might enter directions to each person’s house. What issues come up regarding versioning and extensibility? Which form was easier to modify? What about converting existing data?

Design a small address book database (name, phone number, and so on) using a straightforward binary representation in your language of choice. Do this before reading the rest of this challenge.

Translate that format into a plain-text format using XML or JSON.

Translate that format into a plain-text format using XML or JSON.

For each version, add a new, variable-length field called directions in which you might enter directions to each person’s house.

For each version, add a new, variable-length field called directions in which you might enter directions to each person’s house.

directions

What issues come up regarding versioning and extensibility? Which form was easier to modify? What about converting existing data?

