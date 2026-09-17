# ch010

## Namespaces (Stateless Grouping)


If you group a set of related functions together, without data, then you don’t really have the expected encapsulation a module implies. The better term for this grouping of stateless functions is a namespace:

Utils here is a useful collection of utilities, yet they’re all state-independent functions. Gathering functionality together is generally good practice, but that doesn’t make this a module. Rather, we’ve defined a Utils namespace and organized the functions under it.
