---
github: awesome_javascripts
---

<kbd class="imgtitle">Contents</kbd>

- [Introduction](#overview)
- [Basic Scripts](#scripts)
- [Functions](#functions)
- [Oop in JS](#oop-in-js)
- [DOM](#dom---document-object-model)
- [AJAX](#ajax)
{: .contentBorder .txt-pad}


## Introduction
---
- JavaScript is a web language which adds dynamism to the web page.
- Brendan Eich (**NetScape**) created JS in *Mozilla*.
- Created in light weight and not to show errors to the user by using intelligent guessing.
- ECMA (European Computer Manufacturers Association) standardizes JS.

## Scripts
---

**Note :** Use Browser console logs to see outputs, while script requires.

- **[Alerts](#alerts)**
- **[Variable](#variable)**
- **[REPL](#repl)**
- **[DataTypes](#datatypes)**
- **[Operators](#operators)**
- **[if-else statement](#if-statement)**
- **[Switch](#switch)**
- **[Object - Data Type](#object)**

###### Alerts
---

```html
<head>
<script>
	alert("Hello world !");
</script>
</head>
```


###### Variable
---

```html
<head>
<script>
	var info = "Hi by variable";
	info += "\nSo Hello world"
	alert(info);
</script>
</head>
```

**Note : Type Conversion**
- "4" * "3" == 12
- "4" + "2" == 42

###### REPL
---
**REPL - Read Eval Print Loop**

```html
<head>
<script>
	var info = "Hi by variable";
	info += "\nSo Hello world"
	alert(info);
	console.log(info);
</script>
</head>
```
###### DataTypes
---

**Types :**
- Primitive
    - Number
    - String
    - Boolean
- Object
    - Objects
    - Functions
- NULL

```html
<head>
<script>
	var x;
	var p = "Now x is : "
	console.log(p + typeof x);

	// datatype : number
	x = 5;
	console.log(p + typeof x);
	
	// datatype : null (special)
	x = null;
	console.log(p + typeof x);

	// datatype : string
	x = "Hi by variable";
	console.log(p + typeof x);

	// Using comments like this line
	// checking for Booleans data type
	x = false;
	var y;
	function chekBool(z){
		if(z){
			console.log(z + ' is True Type.')
		}else{
			console.log(z + ' is False Type.')
		}
	}
	chekBool(x);
	chekBool(y);
	y = 'String';
	chekBool(y);
</script>
</head>
```
**Note :** 
- Each char in String uses *16 Bits* for storage.
- Each number uses **64 Bit** floating point type.

###### Operators
---

|Operators|||||
|-|-|-|-|-|
|Arithmetic|+|-|*|/|%|
|Conditional|<|<=|>|>=||
|Incre/ Decre|++|--||||
{: .dataframe style="width: 75%;margin-left: 10%;"}

###### If Statement
---

```html
<head>
<script>
	function isEven(z){
		if(z%2 == 0){
			alert(z + ' is Even.');
		}else{
			alert(z + ' is Odd.');
		}
	}
	var x = "0";
	isEven(x);
</script>
</head>
```

###### Switch
---

```html
<head>
<script>
	function isEven(z){
        switch(z){
            case z % 2 == 0: return true;
                break;
            default: return false;
        }
	}
	var x = "0";
	isEven(x);
</script>
</head>
```

###### Loops
---

1. For Loop
1. While Loop

Using <mark>break</mark> and <mark>continue</mark> also explained.

```html
<head>
<script>
    var i=0;
    while (i <= 10)
    {
    	i++;
    	if (i == 5){break;}
    	if (i == 3){continue;}
        console.log('While Loop Iteration : '+i)
    }
    
    for (var j=1; j<=5 ;j++){
        console.log('For Loop Iteration : '+j);
    }
</script>
</head>
```

###### Scripts Note:
---

We can use external script file inside the html as for organizing the
code and the build healthier.

```html
//script used for IE9 browser.
<script src="http://html5shiv.googlecode.com/svn/trunk/html5.js"></script>
// Local js
<script src="path/to/your/all.js"></script> 
```

###### Object
---

\# In Browser Console:

```html
var x = new Object();
x.name = "chitti"
x.version = "2.0"
console.log(x);
```
**Output** : {name: "2.0", version: "2.0"}

###### JSON
---

Normally JSON Object would be like,

```json
{
  "root": {
    "binaries": {
        "0": {
            "val": "0"
        },
        "1": {
            "val": 1
        }
    },
    "ternaries": [0, 1, 2]
  }
}
```
Some rules are there .. such as...

- A number can't be a key for the object.

Initially it should look like a complex structure. Do some play with
json to familiar with it.

###### List Operations
---

Types :

- Basics
    - Sort
- Comprehension
    - Filter
    - Map
    - Reduce

```java
var x = [1,2];
x.unshift(0)
// x = [0,1,2]
x.shift()
// x = [1,2]
x.push(3)
// x = [1,2,3]
x.pop()
// x = [1,2]
x = [1,2,3,4,5,6]
var s = x.slice(3,7)
//s = [4, 5, 6]
x.splice(3)
// x = [4, 5, 6]
```

###### Sort :
---

```java
var x = [1, 2, 5, 6, 10, 2, 7];
x.sort()
// Output : [1, 10, 2, 2, 5, 6, 7]

function sort_asc(a,b){ return (a-b)}
function sort_desc(a,b){ return (b-a)}

x.sort(sort_asc);
// Output : [1, 2, 2, 5, 6, 7, 10]
x.sort(sort_desc);
// Output : [10, 7, 6, 5, 2, 2, 1]
```

###### Filter :
---

```java
var x = [1, 2, 5, 6, 10, 2, 7];
x.filter(function(x){return x % 2 == 0})

x.filter(function v(val, id, li){ console.log(val, id, li)})
```

[2, 6, 10, 2]
1 0 [1, 2, 3, 4]
2 1 [1, 2, 3, 4]
3 2 [1, 2, 3, 4]
4 3 [1, 2, 3, 4]
{: .output}

###### Map :
---

```java
var x = [1, 2, 5, 6, 10, 2, 7];
x.map(function(x){return x / 2})
```

[0.5, 1, 2.5, 3, 5, 1, 3.5]
{: .output}

###### Reduce :
---

```java
var x = [1, 2, 5, 6, 10, 2, 7];
x.reduce(function(prev, curr){console.log(prev, curr);prev = curr; return prev},0)
```

0 1
1 2
2 3
3 4
4
{: .output}
{: .output}

## Functions
---

- A function can be used as an argument to another function.
- As arguments, a function can be returned from another function.

###### content :

- [Higher Order](#higher-order)
- [Anonymous](#anonymous)
- [Nested](#nested)
- [Closures](#closure)
- [Argument Parse](#argument-parse)

###### Higher Order
---

```java
function is_even(x){ 
    return x % 2 == 0
}

function a(filter){ 
    var li = [1,2,3,4]; 
    for (var x of li){
        if(filter(x)){ 
            console.log(x)
        }
    }
}

a(is_even)
```


2
4
{: .output}

###### Anonymous
---

```java
var li = [1,2,3,4]; 
li.forEach(
        function (i){ console.log(i)}
        )
```

1
2
3
4
{: .output}

###### Nested
---

```java
function hypotenuse (a, b){
    function sq(x) { return x*x }
    return Math.sqrt(sq(a)+sq(b))
}
```

###### Closure
---

```java
function stepiter (start, step){
    return function (){
        var x = start;
        start += step;
        return x;
    }
}
var iter = stepiter (3,6);
iter()
iter()
iter()
```

3
9
15
{: .output}

###### Argument Parse
---

- Converting Multiple arguments into Array

```java
function mul_to_arr(){
    return Array.prototype.slice.call(arguments)
}
mul_to_arr(1,2,3,4)
```

[1,2,3,4]
{: .output}

## OOP In JS
---

- [This](#this)
- [Constructor and Prototype](#constructor-and-prototype)

###### This
---

```java
var square = { side : 4, area : function (){ return (this.side * this.side)}, perimeter : function() { return 4 * this.side;}}
square.area()
square.perimeter()

var square = { side : 4, area : (this.side * this.side), perimeter : (4 * this.side)}
square.area
square.perimeter
```

16
16
NaN
NaN
{: .output}

###### Constructor and prototype
---

```java
function Square(x){ this.side = x; this.area = function (){ return this.side * this.side};}
var x = new Square(3)
console.log(x.area())
Square.prototype.perimeter = function() { return (4 * this.side)}
console.log(s.perimeter())
```

9
8
{: .output}

###### Others :
---

- SetTimeOut

```commandline
setTimeout(function() {console.log("Delay time 5s over. The line printed.")},5000)
```

Delay time 5s over. The line printed.
{: .output}

## DOM - Document Object Model
---
The DOM model represents a document with a logical tree like <mark>XML</mark> and <mark>HTML</mark>.

**document**
    **|__html**
        **|__head**
        **|   |__ . . .**
        **|__body**
            **|__ . . .**
{: .output}

Some methods are :

- document.getElementById()
- document.getElementsByClassName()
- document.getElementsByName()
- document.getElementsByTagName()

For example we can change the document by Java script like shown below,

document.getElementById("testElem").style.display = "block";
{: .output}

## AJAX
---

AJAX - **Asynchronous Java Script and XML**

Without reloading the web page, we can communicate to the server using **AJAX** and can update the page. 
For example, by clicking a button will load a **function()** and that will do the rest.

```groovy
var xhttp = new XMLHttpRequest();
xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      console.log(this.responseText);
    }
  };
xhttp.open("GET", "additional.html", true);
xhttp.send()
```