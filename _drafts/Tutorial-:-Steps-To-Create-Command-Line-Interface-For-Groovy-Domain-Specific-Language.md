---
github: dsl
---

<kbd class="imgtitle">Contents</kbd>

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Step 1: ](#)
- [Oop in JS](#oop-in-js)
- [DOM](#dom---document-object-model)
- [References](#references)
{: .contentBorder .txt-pad}

## Introduction
---

Even there are many ways to do this, Here I have posted a simple method to grab the concept quickly for 
the tutorial. As this post not need that much introduction, we can directly start with steps shown below,

- Prerequisites
- Organize the directory
- Implement source code
- Implement software code
- Build Strategy
- Release

## Prerequisites
---

The prerequisites are,

|Name of the Package|Version|
|----|-------|
|Java|1.8.0|
|Groovy|2.4.15|
|Gradle|4.10.2|
{: .dataframe}

Also set the environment variables according to the packages which are,

- <mark> JAVA_HOME </mark>
- <mark> GROOVY_HOME </mark>

## Organize the Directory
---

Initially, Organize the source code directory like shown below,

```commandline
- software
    - bin
    - examples
- src
    - main
        - groovy
            - path/of/package
                - subdir1
                    - implementation1.groovy
                - subdir2
                    - implementation2.groovy
```

So here, It contains two areas.
- **Source** 
    
    We always works here to create a package or Jar to use.

- **Software**
    
    This is going to have the **Command Line Entry Points**. This can be configured by our own style of coding.
    
## Implement Source Code
---

As a command Line Interface