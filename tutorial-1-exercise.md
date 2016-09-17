## Tutorial 1: Accessing the DOM

#### Exercise: Tree Walker

One final detail is that the firstChild, lastChild, previousSibling, nextSibling, and parentNode properties return null if there is no such child, sibling or parent node. Likewise, the childNodes array is of length zero if there are no child nodes.
You now know the API for navigating your way around any DOM tree. For this exercise, put all these pieces together to write a function called nextNode that can be used to walk through all the nodes of a DOM tree. The function should take a node as an argument, and return the next node in the tree. For example, the following loop would visit every node once, and only once:

``` javascript
var node = document.body;
do {
  node = nextNode(node);
} while (node != null)
```

This is not an easy exercise, it requires careful thought. Beware of infinite loops which may crash your browser.

Test your nextNode function by repeatedly clicking the "Execute single step" button. It will highlight each node in sequence, starting with the title of this exercise. Elements (which correspond with HTML tags) receive a green border, text nodes receive a green background.

Solution:
``` javascript
nextNode = function(node) {
  if (node.firstChild) {
    return node.firstChild;
  }
  while (node) {
    if (node.nextSibling) {
      return node.nextSibling;
    }
    node = node.parentNode;
  }
  return node;
};
```