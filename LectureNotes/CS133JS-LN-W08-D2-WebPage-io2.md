---
title: Web page i/o 2
description: Accessing web page DOM elements and using events.
keywords: DOM, innerHTML, getEelmentById, textContent, event, event handler
material: Lecture Notes
generator: Typora
author: Brian Bird
---

**CS133JS Beginning Programming: JavaScript**

<h1>The Document Object Model</h1>


| Topics by Week                           |                                    |
| ---------------------------------------- | ---------------------------------- |
| 1. Intro to JavaScript programming       | 6. Arrays                          |
| 2. Functions, Operators and Expressions  | 7. Objects and Object Constructors |
| 3. Conditional Statements: if and switch | 8. <mark>Web Page I/O</mark>       |
| 4. Repetition: while, do while, and for  | 9. Dynamic Web Pages               |
| 5. Midterm Check-Point                   | 10. Review for final quiz          |


<h2>Table of Contents</h2>

[TOC]

## Introduction

### Q and A

- Any questions?



## Review (with some Additions)

### The DOM

The DOM is a set of JavaScript objects that represent the web page and all its HTML elements. 

![DOM-model](../Images/DOM-model.svg)

By <a href="//commons.wikimedia.org/w/index.php?title=User:Eib&amp;action=edit&amp;redlink=1" class="new" title="User:Eib (page does not exist)">Birger Eriksson</a> - <span class="int-own-work" lang="en">Own work</span>, <a href="https://creativecommons.org/licenses/by-sa/3.0" title="Creative Commons Attribution-Share Alike 3.0">CC BY-SA 3.0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=18034500">Link</a>

#### Accessing DOM Objects

##### Directly accessing elements

Each object in the diagram above has an array of children. We don't normally access these directly, but we can. For example, the code below will change the text in the `<h1>` element: 

```javascript
document.children[0].children[1].children[0].textContent = "New Heading";
```

If you want to explore the hierarchy of DOM objects, you can do it fairly easily in the console.

##### Accessing elements using `getElementById`

Returns a reference to an HTML element.

```javascript
let lccElement = document.getElementById("lcc");
```

#####  Accessing elements using `querySelector` 

Returns a reference to the first matching element it finds on the page. 

```javascript
let lccElement = document.querySelector("#cit");
let degreeElement = document.querySelector("#s1 p span");
```



### I/O Using HTML Elements

#### `innerHTML`

A property used to get or set the text and any HTML tags between the tags of an element.

```javascript
document.getElementById("ex").innerHTML = "<u>This</u> text contains <em>tags</em>."
```

#### `textContent`

A property used to get or set just the text between the tags of an element.

```javascript
document.getElementById("ex").innerHTML = "This is just plain text."
```

#### `value`

This property used to get or set the value of an HTML input element. 

```javascript
let person = document.getElementById("name").value;
```

#### Get User Input with a `<button>` and `onclick`Event Handler

Use a button with an `onclick` *event handler* to get user input.

```html
Enter your name:<input>
<button onclick="inputName()">Enter</button>

<p>Hello: <span id="name"></span></p>
<script>
  function inputName() {
    let name = document.querySelector("input").value;
    document.querySelector("#name").innerHTML = name;
  }
</script>
```





## More on Web Page I/O

Here are some additional tips and techniques for accessing HTML elements using the DOM.

### Accessing HTML Element Attributes

Review: An *attribute* defines some characteristic of an HTML element and is coded as a key value pair. In the example below, `href` is an attribute.

```html
<a href="https://profbird.dev">Your instructor's web site</a>
```

Here is the JavaScript code to change the attribute:

```javascript
document.querySelector("a").href = "https://birdsbits.wordpress.com/";
```

### Getting Collections of Elements

There are four DOM methods you can use to get an array containing multiple element objects. Each of these are listed below along with an example based on this HTML:

```html
<ul>
	<li name="fruit" class="highlight">Apple</li>
	<li name="fruit">Peach</li>
	<li name="vegetable">Pepper</li>   
</ul>
<ol>
	<li name="fruit" class="highlight">Pear</li>
  <li name="vegetable" class="highlight">Onion</li>
	<li name="vegetable">Pepper</li>
</ol>
```

#### `getElementsByName`

```javascript
let vegetables = document.getElementsByName("vegetable");  // an array of vegies
```

#### `getElementsByClassName`

```javascript
let topProduce = document.getElementsByClassName("highlight");  // array of highlighted items
```

#### `getElementsByTagName`

```javascript
let produce = document.getElementsByTagName("li");  // array of all items
```

#### `querySelectorAll`

```javascript
let selectProduce = document.querySelectorAll("ol .highlight");  // array of highlighted items from the ol
```



## More on Event Handlers

### Event Handlers with Parameters

Use single quotes to pass an argument to an event handler that has a parameter. In this example, one button's event handler is passed an `'A'`, the other a `'B'` :

```html
<button onclick="buttonPressed('A')">Button A</button>
<button onclick="buttonPressed('B')">Button B</button>
<p>Button <span></span> was pressed.</p>
<script>
  function buttonPressed(letter) {
    document.querySelector("span").textContent = letter;
  }
</script>
```

### Adding an Event Handler to an Element Using JavaScript

You can add an event hander to an HTML element in JavaScript rather than adding it as an attribute of the element.

```html
<button>Click me</button>
<p><span></span></p>

<script>
  document.querySelector("button").addEventListener("onclick", buttonPressed);
  
	function buttonPressed() {
			document.querySelector("span").textContent = "Button pressed!";
  }
</script>
```

You can also define an *anonymous function* when adding the event listener:



```html
<button>Click me</button>
<p><span></span></p>

<script>
  document.querySelector("button").addEventListener("onclick", function () {
			document.querySelector("span").textContent = "Button pressed!";
  });
</script>
```

If you want to add a function that has parameters to an HTML element, you need to wrap that function in an anonymous function, like this:

```html
<button>Button A</button>
<p><span></span></p>

<script>
  document.querySelector("button").addEventListener("onclick", function () {
			buttonPressed("A");
  });
                                                    
  function buttonPressed(letter) {
    document.querySelector("span").textContent = letter;
  }
</script>
```



### Running Code after the Page Loads with the `onload` Event

Sometimes need to execute some code as soon as the page loads. The example below reads the contents of an array and puts it into a list on the web page. Note that the `listTrees()` function could also be in a separate .js file.

```html
<body onload="listTrees()"> 
  <script>
    let trees = ["Oak", "Pine", "Cedar", "Fir", "Birch"];
    function listTrees() {
      for (tree of trees) {
        document.querySelector("ol").innerHTML += "<li>" + tree + "</li>";
      }
    }
  </script>
  <ol>
  </ol>
</body>


```



## Reference

[DOM (Document Object Model)](https://developer.mozilla.org/en-US/docs/Glossary/DOM)&mdash;MDN

[Event Reference](https://developer.mozilla.org/en-US/docs/Web/Events)&mdash;MDN

[JavaScript HTML DOM Event Listener](https://www.w3schools.com/js/js_htmldom_eventlistener.asp)&mdash;W3Schools

------

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/) Beginning JavaScript Lecture Notes by [Brian Bird](https://profbird.online), <time>2022</time>, are licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/). 