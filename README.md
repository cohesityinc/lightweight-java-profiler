# lightweight-java-profiler

> the project is forked from code.google.com/p/lightweight-java-profiler

## GettingStarted  

### Introduction

This document contains information on how to use the profiler.

<del>

### Details

First, check out the profiler:

> svn checkout http://lightweight-java-profiler.googlecode.com/svn/trunk/ lightweight-java-profiler-read-only
 
Then change into the directory, and build:

> cd lightweight-java-profiler-read-only
> make all

</del>

### build

#### install dependencies

```
sudo apt-get install gcc g++ g++-multilib
```

#### make 

```
make all
```

It defaults to a 32-bit build; it will place the resulting liblagent.so file in the build-32 directory; if you want to have a 64-bit build, say "make BITS=64 all" instead.

To use the profiler, you can invoke Java as follows:

> java -agentpath:path/to/liblagent.so[:file=fname] <jvm flags>

It will spit out stack traces into traces.txt (or into the optional fname passed to the agent). The current implementation samples every 1/100th of a second. It stores the first 3000 stack traces it encounters; additional stack traces will be ignored, but duplicate stack traces will continue to be counted indefinitely (or until the counter overflows, which will take a while).

Yes, this is a horrible user interface. I imagine it would be relatively straightforward to spit out results in dot, or create any interface you want for parsing the output. Patches welcome.


### gen Flame Graph

```
git clone http://github.com/brendangregg/FlameGraph
cd FlameGraph
./stackcollapse-ljp.awk < ../traces.txt | ./flamegraph.pl > ../traces.svg
```

more detail see http://www.brendangregg.com/blog/2014-06-12/java-flame-graphs.html
