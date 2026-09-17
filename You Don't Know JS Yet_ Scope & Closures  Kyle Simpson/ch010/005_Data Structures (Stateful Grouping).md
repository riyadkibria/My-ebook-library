# ch010

## Data Structures (Stateful Grouping)


Even if you bundle data and stateful functions together, if you’re not limiting the visibility of any of it, then you’re stopping short of the POLE aspect of encapsulation; it’s not particularly helpful to label that a module.

Since records is publicly accessible data, not hidden behind a public API, Student here isn’t really a module.

Student does have the data-and-functionality aspect of encapsulation, but not the visibility-control aspect. It’s best to label this an instance of a data structure.
