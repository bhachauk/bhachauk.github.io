<kbd class="imgtitle">Contents</kbd>

- [Objective](#objective)
- [Simple overview](#simple-overview)
- [GC Roots](#gc-roots)
- [How to Collect?](#how-to-collect)
- [Tools](#tools)
- [By program](#by-program)
{: .contentBorder .txt-pad}

### Objective
---

Knowing about Heap dump and also learn about the methods, what are all the parsing techniques
available.

### Simple Overview
<hr>

We know that <mark>Java</mark> byte codes are executed by <mark>JVM</mark> or <mark>Java Virtual Machine</mark> . 
JVM uses some os memory for all its need and part of this memory is called <mark> java heap memory</mark> .
whenever we create an object using new operator or by any another means the object is allocated memory from Heap and 
When object dies or garbage collected, memory goes back to Heap space.

<div class="imgbrd">
<p align="center">
  <img src="/images/post_img/heap.png" align="center"/>
</p></div>

Garbage collection is a mechanism provided by Java Virtual Machine to reclaim heap space from objects 
which are eligible for Garbage collection. Garbage Collection in Java is carried by a daemon thread called <mark>Garbage Collector</mark>.

So by overall, Garbage collection is responsible for,

- Allocating memory.
- Ensuring that any referenced objects remain in memory.
- Recovering memory used by objects that are no longer reachable from references in executing code. 

Special objects called garbage-collection roots or GC Roots are used to form a reachable tree.

<p class="noteHeader">Any object that has a garbage-collection root at its own root</p>

### GC Roots
---

###### Types of GC Roots

Four types of GC roots:

- Local variables.
- Active threads.
- Static variables.
- JNI references.

<kbd class="imgtitle">GC Roots</kbd>

![classLoaders](/images/post_img/class_loaders.jpg)
{: .imgbrd}

See Source : <a class="link" href="https://www.w3resource.com/java-tutorial/garbage-collection-in-java.php">link</a>

### How to Collect
<hr>

Using <mark>jmap</mark>  command.

```
    jmap -dump:format=b,file=/tmp/heap.hprof pid
```

To find the java process pids alone, Use the command,

```
    ps -C java -o pid
```

So after executing this commands the java heap dump file will be saved in <mark>/tmp/heap.hprof</mark>  

### Tools
<hr>

- <a class="link" href="http://www.eclipse.org/mat/downloads.php">MAT</a>
- <a class="link" href="https://www.ibm.com/developerworks/community/groups/service/html/communityview?communityUuid=4544bafe-c7a2-455f-9d43-eb866ea60091">IBM Heap Analyzer</a> 
- <a class="link" href="https://docs.oracle.com/javase/6/docs/technotes/tools/share/jvisualvm.html">JVISUALVM</a>

I personally like *IBM Heap Analyzer*.

### By program
<hr>

I found this [GitHub Repo](https://github.com/aragozin/jvm-tools/tree/master/hprof-heap) for parsing the heap dump.

It is really awesome. See the repo <a class="link" href="http://blog.ragozin.info/2015/02/programatic-heapdump-analysis.html">blog</a>