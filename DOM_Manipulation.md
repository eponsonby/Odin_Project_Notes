# What is the DOM?
- The Document Object Model is a tree-like representation of the contents on a webpage or document - a tree of "nodes".
- One of the most useful abilities of JavaScript is the ability to manipulate the DOM
- The DOM is the browsers internal programmatic representation of the web page. It can be manipulated by languages like JS, changing the page without changing the HTML
- [From Wikipedia:](https://en.wikipedia.org/wiki/Document_Object_Model) it is an API (application programming interface) that treats an HTML or an XML document as a tree structure wherein each node is an object representing part of the document. DOM methods allow programmatic access to the tree; with them one can change the structure, style, or content of a document. Nodes can have event handlers attached to them. 
- ![DOM Model](https://www.w3schools.com/js/pic_htmltree.gif "DOM Model")

``` html
<div id="container">
    <div class="display"></div>
    <div class="controls"></div>
</div>
```
In the above example `<div class="display></div>` is a "child" of `<div id="container"></div>` and sibling to `<div class="controls"></div>`. Think of it like a family tree `<div id="container"></div>` is a **parent** with its children on the next level, each on their own "branch"


## Node vs. Element
- A node is any object in the DOM hierarchy. Nodes can include elements, text content inside an element, code comment blocks, the document itself and even abstract types like “fragments”
- An element is ONE specific node

## How do you target nodes with selectors?
- When working with the DOM you use "selectors" to target the nodes you want to work with. You can use a combo of CSS-style selectors and relationship properties to target the nodes you want.
- There are several ways with CSS style-selectors to target a node
- `<div class=”display”</div>` can be selected as follows
  * `div `
  * `div.display`
  * `.display`
  * `#container>.display`
  * `div#container>div.display`
- There are also relational selectors such as `firstChild` and `lastSibling`
- Combined with “Query Selectors” this is how you target a node using JS
- i.e. `document.querySelector(“.display”)`; would select the div above

## DOM Methods
- When your HTML is parsed by the browser, it is converted to the DOM. Primary diff is these nodes are objects that have many properties and methods attached to them. These properties and methods are the primary tools we are going to use to manipulate our webpage with JS. Starting with Query Selectors - those that help you target the nodes

### Query Selectors
- As mentioned above, you can find nodes in the DOM using query selectors
- `element.querySelector(selector)` returns reference to the first match of *selector*
- `element.querySelectorAll(selector)` returns a "nodelist" containing references to all of the matches of the selectors.
  * When using querySelectorAll, the return value is **not** an array, although it looks like one. You can convert the nodelist into an array using Array.from() or the spread operator

### Element Creation 
- To create an element, use `document.createElement(tagName[, options])`. This method creates the HTML element specified by tag name. Options means you can add some optional parameters to the function (don't worry about this right now)
```javascript
  const div = document.createElement(‘div’)
  ```
- The above will create a div element. However this div has not been added to the webpage yet (the function does not put your new element into the DOM - it creates in memory so you manipulate the element before placing it on the page). To actually place it on the page, use one of the following methods:

### Append Elements
- `parentNode.appendChild(childNode)` appends childNode as the last child of parentNode
  * i.e `parentNode.appendChild(div);`
- `parentNode.insertBefore(newNode,referenceNode)` inserts newNode into parentNode before referenceNode

### Remove Elements
- `parentNode.removeChild(child)` removes child from parentNode on the DOM and returns reference to child
  * i.e. `parentNode.removeChild(div);`

### Altering Elements
- Once you have a reference to an element you can use that reference to alter the element's own properties. This allows you to do many useful alterations like adding/removing and altering attributes, changing classes, adding inline style info, etc.
``` javascript
const div = document.createElement('div')
// create a new div referenced in the variable 'div'
```
- Adding inline style
``` javascript
div.style.color = 'blue';
// adds the indicated style rule
div.style.cssText = 'color: blue; background: white';
// adds several style rules
div.setAttribute('style', 'color: blue; background: white');
// adds several style rules
```

### Editing Attributes
``` javascript
div.setAttribute('id', 'theDiv');
// If id exists, update it to 'theDiv' else create an id with value 'theDiv'
div.setAttribute('id');
// returns the value of specified attribute, in this case, 'theDiv'
div.removeAttribute('id');
// removes specified attribute
```
### Working with Classes
``` javascript
div.classList.add('new');
// adds class 'new' to your new div
div.classList.remove('new');
// remove 'new' class from div
div.classList.toggle('active');
// if div doesn't have class 'active' then add it. If it does, remove it
```
- It is often standard and more clean to toggle a CSS style rather than adding/removing inline css

### Adding Text Content
``` javascript
div.textContent = 'Hello, World!'
// creates a text node containing 'Hello, World!' and inserts it in div
```

### Adding HTML Content
``` javascript
div.innerHTML = '<span>Hello World!</span>';
// renders the HTML inside div
```
- textContent is preferable for adding text; innerHTML should be used sparingly

## What is the difference between a "nodelist" and an "array of nodes"?
- A "nodelist" looks like an array, but it is missing several methods that come with an array
- A solution to this problem is to use the spread operator or Array.from() to convert a nodelist into an array

## How do "events" and "listeners" work?
- "Events" are how you make your webpage dynamic. They are triggered by "listeners", and can fire when the page loads, when you click your mouse, when you push keys on your keyboard and more
- There are three primary ways to use events
  * By attaching scripts to event attributes on elements in the HTML document
  * `<button onclick ="alert(this.tagName)">Click Me</button>`
  * By setting the "on_event" property on the DOM object in your JS
  ```html
  // the html file
  <button id="btn">Click Me</button>
  ```
  ``` javascript
  // the javascript file
  var btn = document.querySelector('#btn');
  btn.onclick = (e) => alert(e.target.tagName);
  ```
  * By attaching event listeners to the nodes in your JavaScript
  ``` html
  // the html file
  <button id="btn">Click Me Too</button>
  ```

``` javascript
// the JavaScript file
var btn = document.querySelector('#btn');
btn.addEventListener(‘click’, (e) => {
  alert(e.target.tagName);
});
```
## How does bubbling work?
- Bubbling is a form of "event propagation"
- It is an efficient method for firing an event on multiple elements - starting from the innermost element - and "bubbling up" to outer elements