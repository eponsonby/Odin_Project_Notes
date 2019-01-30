**What is the DOM?**
- The Document Object Model is a tree-like representation of the contents on a webpage or document.
- One of the most useful abilities of JavaScript is the ability to manipulate the DOM

**Node vs. Element**
- A node is any object in the DOM hierarchy. Nodes can include elements, text content inside an element, code comment blocks, the document itself and even abstract types like “fragments”
- An element is ONE specific node

**How do you target nodes with selectors?**
- There are several ways with CSS style-selectors to target a node
- `<div class=”display”</div>` can be selected as follows
  * `div `
  * `div.display`
  * `.display`
- There are also relational selectors such as `firstChild` and `lastSibling`
- Combined with “Query Selectors” this is how you target a node using JS
- i.e. `document.querySelector(“.display”)`; would select the div above

**Basic methods for finding/adding/removing and altering DOM nodes**
- As mentioned above, you can find nodes in the DOM using query selectors
- To create an element, use `document.createElement(tagName[, options])` 
  * `const div = document.createElement(‘div’)`; will create a div element. However this div has not been added to the webpage yet
- To append this element, use `parentNode.appendChild(childNode)`
  * i.e `parentNode.appendChild(div);`
- To remove this element, `parentNode.removeChild(child)`
  * This will remove child from parentNode on the DOM and returns reference to child
  * i.e. `parentNode.removeChild(div);`
- Once you have a reference to an element, as above, you can alter it in many ways
  * `div.style.color = 'blue';`
  * `div.setAttribute('id', 'theDiv');` sets the id attribute of our div to `theDiv`

**What is the difference between a "nodelist" and an "array of nodes"?**
- A "nodelist" looks like an array, but it is missing several methods that come with an array
- A solution to this problem is to use the spread operator or Array.from() to convert a nodelist into an array

**How do "events" and "listeners" work?**
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