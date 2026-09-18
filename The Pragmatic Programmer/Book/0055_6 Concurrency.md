# 6 Concurrency


**Source File:**

None


**Word Count:**

None



---

Chapter 6

Concurrency

Just so we’re all on the same page, let’s start with some definitions:

Concurrency is when the execution of two or more pieces of code act as if they run at the same time. Parallelism is when they do run at the same time.

Concurrency

Parallelism

To have concurrency, you need to run code in an environment that can switch execution between different parts of your code when it is running. This is often implemented using things such as fibers, threads, and processes.

To have parallelism, you need hardware that can do two things at once. This might be multiple cores in a CPU, multiple CPUs in a computer, or multiple computers connected together.

