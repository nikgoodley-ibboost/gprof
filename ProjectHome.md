### OVERVIEW ###

The Groovy profiler, **GProf** is a profiling module for [Groovy](http://groovy.codehaus.org/). It allows you
to determine which parts of a program are taking most of the execution time
as the GNU profiler, gprof does for C and C++. GProf is a sub-project of **[GPerfUtils](http://gperfutils.org)**.

### VERSIONING ###

GProf has different versions for different Groovy versions.
```
  [major].[minor].[maintenance]-groovy-[groovy_major].[groovy_minor]
```

For example, the versions of GProf 0.3.1 that supports from Groovy 2.0
to Groovy 2.4 are:
```
  0.3.1-groovy-2.0, 0.3.1-groovy-2.1, 0.3.1-groovy-2.2, 0.3.1-groovy-2.3, 0.3.1-groovy-2.4
```


---


### DOWNLOADING ###

Download a distribution from the Maven Central repository using a
dependency manager of your choice.

Groovy Grape
```
  @Grab(group='org.gperfutils', module='gprof', version='[version]')
```

Apache Maven
```
  <dependency>
    <groupId>org.gperfutils</groupId>
    <artifactId>gprof</artifactId>
    <version>[version]</version>
  </dependency>
```

Apache Ivy
```
  <dependency org="org.gperfutils" name="gprof" rev="[version]" />
```

### BUILDING ###

Download the source from [the repository](https://github.com/gperfutils/gprof) and build using Ant.

Distribution
```
  ant dist
```

Binary jar for a specific Groovy version
```
  ant binary -Dgroovy.version=[groovy_version]
```


---


### EXAMPLE ###

```
// slow !!
def fib(n) {
    if (n < 2) {
        n
    } else {
        fib(n - 1) + fib(n - 2)
    }
}

profile {
    fib(20)
}.prettyPrint()
```
stdout:
```
Flat:

 %    cumulative   self            self     total    self    total   self    total
time   seconds    seconds  calls  ms/call  ms/call  min ms  min ms  max ms  max ms  name
54.3        0.29     0.29      2   145.86   267.78   38.14   58.56  253.57  477.00  demo.fib
30.4        0.45     0.16  21890     0.00     0.00    0.00    0.00    0.80    0.80  java.lang.Integer.minus
15.0        0.53     0.08  10945     0.00     0.00    0.00    0.00    0.83    0.83  java.lang.Integer.plus
 0.1        0.53     0.00      1     1.05   537.10    1.05  537.10    1.05  537.10  demo$_run_closure1.fib
 0.0        0.53     0.00      1     0.13   537.23    0.13  537.23    0.13  537.23  demo$_run_closure1.doCall

Call graph:

index  % time  self  children  calls        name
               0.00      0.53          1/1      <spontaneous>
[1]     100.0  0.00      0.53            1  demo$_run_closure1.doCall [1]
               0.00      0.53          1/1      demo$_run_closure1.fib [2]
-----------------------------------------------------------------------------
               0.00      0.53          1/1      demo$_run_closure1.doCall [1]
[2]      99.9  0.00      0.53            1  demo$_run_closure1.fib [2]
               0.29      0.24          2/2      demo.fib [3]
               0.00      0.00      2/21890      java.lang.Integer.minus [4]
               0.00      0.00      1/10945      java.lang.Integer.plus [5]
-----------------------------------------------------------------------------
               0.29      0.24          2/2      demo$_run_closure1.fib [2]
[3]      99.6  0.29      0.24      2+21888  demo.fib [3]
               0.16      0.00  21888/21890      java.lang.Integer.minus [4]
               0.08      0.00  10944/10945      java.lang.Integer.plus [5]
-----------------------------------------------------------------------------
               0.00      0.00      2/21890      demo$_run_closure1.fib [2]
               0.16      0.00  21888/21890      demo.fib [3]
[4]      30.4  0.16      0.00        21890  java.lang.Integer.minus [4]
-----------------------------------------------------------------------------
               0.00      0.00      1/10945      demo$_run_closure1.fib [2]
               0.08      0.00  10944/10945      demo.fib [3]
[5]      15.0  0.08      0.00        10945  java.lang.Integer.plus [5]
-----------------------------------------------------------------------------
```

Other examples are available [here](https://github.com/gperfutils/gprof/tree/master/src/demo).

### SUPPORT ###

Groovy Versions: 2.0, 2.1, 2.2, 2.3, 2.4

### NEWS ###

  * 2015-06-27 v0.3.1 released (only for supporting Groovy 2.4)
  * 2013-09-14 v0.3.0 released [ReleaseNotes030](ReleaseNotes030.md)
  * 2013-04-14 v0.2.0 released [ReleaseNotes020](ReleaseNotes020.md)
  * 2013-04-03 GProf was born!