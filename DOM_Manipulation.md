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
