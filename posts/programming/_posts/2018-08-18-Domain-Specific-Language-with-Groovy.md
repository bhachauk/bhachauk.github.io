---
github: dsl
oneliner: Your Own Language in Your Own World - Essense of Groovy
---

<kbd class="imgtitle">Contents</kbd>

1. [Introduction](#dsl---an-introduction)
1. [Simple Implementation in Java](#simple-implementation-in-java)
1. [Converting as DSL](#converting-as-dsl)
1. [Build as DSL](#build-as-dsl)
1. [Sample DSL Codes](#sample-dsl-codes)
1. [Advantages](#advantages)
{: .contentBorder .txt-pad}

## DSL - An Introduction
<hr>

Normally, we are looking for a language which reflects our working domain. But the support
and enhancement of that domain language is difficult to get. Programming languages like Java, has
a big support and almost all libraries. So wrapping up a normal programming language for 
a specif domain with our own derived <mark>keywords</mark> will be considered as a <mark>DSL</mark>.

###### Examples
---

<mark>Gradle</mark> is a good example for <mark>DSL</mark> which is used for build jobs.

<mark>Jenkins pipeline</mark> also a build automation DSL used as a <mark>plugin</mark>.

###### Ready Up ..!
---

If you are new to <mark>Groovy</mark>, First go through basics such as,

- [Difference between Java and Groovy](http://groovy-lang.org/differences.html) : Official documentation
- [Integration](http://groovy-lang.org/integrating.html) 
- Find my Repo [Learn Groovy](https://github.com/bhachauk/Learn_Groovy.git) for Groovy snippets below,
 
## Simple Implementation in Java
---

Let us start with a task for collecting animals list in a zoo. How would be the code in <mark>Java</mark>
for this task.

Java
{: .longTag}

```java
import java.util.ArrayList;
class Animal
{
    String name;
    Integer age;
    public Animal(String name, Integer age)
    {
        this.name = name;       
        this.age = age;       
    }
}
public class Animals{
    public static ArrayList<Animal> register = new ArrayList<Animal>();
    public static void addAnimal(String name, Integer age)
    {
        Animal newAni = new Animal(name, age);
        register.add(newAni);
    }
    public static void showRegister()
    {
        System.out.println ("Animals Details : ");
        System.out.println ("--------------------------");
        for (Animal s : register)
        {
            System.out.println ("Animal Name    : "+s.name);
            System.out.println ("Animal Age     : "+s.age);
            System.out.println ("--------------------------");
        }
    }
    public static void main(String[] args)
    {
        addAnimal ("Richard Parker", 17);
        addAnimal ("Wolverine", 50);
        showRegister();
    }
}
```

<br>

## Converting as DSL
---

What if we have a **'Main ()'** method like shown below DSL code,

Groovy
{: .longTag}

```groovy
    def groupA = animals {
        addAnimal ("Richard Parker", 17)
        addAnimal ("Wolverine", 50)
    }
    groupA.showRegister()
```
 
 This **DSL** code seems more intuition and understandable by a non developer too.
 This may seems as **spec/config** file like xml or yaml which we normally have. It can replace those
 spec files with groovy features which is highly recommended for future changes with reduced conflicts.
 
 This can be obtained from below shown <mark>Groovy</mark> code,
 
 Groovy
 {: .longTag}
 
 ```groovy
    Animals animals(Closure cl)
    {
        Animals als = new Animals()
        cl.delegate = als 
        cl()
        als
    }
    class Animals
    {
        ArrayList<Animal> register = new ArrayList<Animal>()
        void addAnimal (String name, Integer age)
        {
            Animal newAni = new Animal(name, age)
            register << newAni 
        }
        void showRegister()
        {
            println "Animals Details :"
            println "--------------------------"                
            register.each { s ->
                println "Animal Name    : $s.name"
                println "Animal Age     : $s.age"
                println "--------------------------"
            }
        }
    }
    class Animal
    {
        String name
        Integer age   
        Animal(String name, Integer age)
        {
            this.name = name 
            this.age = age 
        }
    }
 ```
  Above shown implementation is really have more advantages than a normal <mark>Java<mark>
  code.
  
## Build as DSL
---

Starting with the basic needs of our day to day work will really helps to progress on developing. 
That will be the base of your Dream DSL. So normally we deals with various file formats like <mark>xml</mark>, <mark>json</mark>, 
<mark>yaml</mark>, <mark>csv</mark>, <mark>xlsx</mark> and etc., Groovy has all supports to parse these various types of files such as like,

- XmlSlurper / XmlParser.
- JsonSlurper.
- POI - Parser for xls/xlsx.

Other facilities like, 

- Javax.mail for EMail.
- JDBC for Dabatabases.

We can create a language layer with our own <mark>keywords</mark> over default methods from the libraries. So 
I have created simple template [DSL build](https://github.com/bhachauk/dsl.git) for these general activities and 
hope that it will let you understand the DSL Development in <mark>high level</mark>. 

## Sample DSL Codes
---

These are my sample codes of my own **DSL Language** from shown above repo. Such as for,

- Email
- Excel
- Json
- Files

###### EMail Support

```groovy
mailserver{
    sethost 'smtp.gmail.com'
    login 'bhanuchander210@gmail.com','*******'
    sendmsg{
        to 'example@gmail.com'
        cc 'any@gmail.com'
        bcc 'any@gmail.com'
        subject 'DSL-EMAIL UTIL'
        body'''
                    ....content ..
            '''
        attach 'dsl.groovy'
    }
}
``` 

###### Excel Support

```groovy
excelstudy{
    excelfile 'filename.xls'
    sheetlist() // returns sheetName list
    getheader('sheetName') // returns header list
    getdata('sheetName') // return 2D data with header
    getdata('sheetName',header=true) // return 2D data with header selection
    getdata('sheetName',hader=true,[0,1,2]) // column filter
    getdata('sheetName',hader=true,[0,1]) // column filter
    getdata('sheetName',["col_1","col_2"]) // column selection
    getdata ('sheetName', ["col_1",1,2]) // support for both string and integer
    getdatamap('sheetName') // return map
}
```

###### Json Support

```groovy
jsonstudy{
    jsonfile 'fileName'
    row 'Xpath.to.Node'
    column 'Xpath.to.col1','Xpath.to.col2'
    result{
        printraw()
    }
}
```

###### File Support

```groovy
filestudy {
    inputFile fileName
    filterLine 'Richard Parker'
    result{
        println line
        println getBetweenString ('Name = ')
        println getBetween ('Name = "',1,'"',2)
    }
}
```

We know that, it can be created with our own <mark>debug</mark>, <mark>log trace</mark> methods and the distribution can be attached with any <mark>Java Package</mark>.

###### Advantages
<hr>
  
 - We can always stay closer to the Domain even while coding than our traditional way.
  
 - <mark>Groovy</mark> is dynamic, that means we can compile it in runtime. This is a big plus that makes us to keep groovy 
    files as a <mark>configuration file</mark>. In shown above code, we can use <mark>animals{...}</mark>
    method is a configuration file for keeping the animal information.
  
 - Even a non-developer can understand the code and can develop by their own with a simple
    documentation.
    
 - The Distribution of this DSL builds can be integrated with any java packages which is a <mark>Java Advantage</mark>, makes
   this DSL a independent build, very much reliable and worth for developing. 
    
 Most of the **Java** developers feels these kind of implementation really helps to easily understand the complicated code.