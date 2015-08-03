  * Support multi-threaded applications

  * Support Grape

  * Add includeMethods and excludeMethods options that filter by the name of packages, classes and methods:
> > It supports the following wildcards:
```
| `*` | zero or more characters |
| ? | exactly one character  |
```
> > The following example profile only methods which are of "java.`*`" or "groovy.`*`" package but are not constructors:
```
profile(
    includeMethods: [ "java.*", "groovy.*" ],
    excludeMethods: [ "*.ctor" ]) {
    // code to be profiled
}
```

  * Add includeThreads and excludeThreads options that filter by the name of threads:
> > It supports the following wildcards:
```
| * | zero or more characters |
| ? | exactly one character   |
```
> > The following example profile only methods which are called in the "thread-`*`" thread but not in "thread-2" or "thread-3":
```
profile(
    includeThreads: [ "thread-*" ],
    excludeThreads: [ "thread-2", "thread-3" ]) {
    // code to be profiled
}
```

  * Bug fixes
    * [Issue 3](https://code.google.com/p/gprof/issues/detail?id=3): GProf fails to profile a multi-threaded application
    * [Issue 4](https://code.google.com/p/gprof/issues/detail?id=4): Contains the time of children if the depth is more than two
    * [Issue 6](https://code.google.com/p/gprof/issues/detail?id=6): There are classes that are not profiled