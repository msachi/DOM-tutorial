## Tutorial 3: DOM Events

#### Lesson: Event object

Here is a table containing 100 stars.
						
This is the HTML for the table to the left:

``` html
<table id="star_table">
  <tr>
    <td><img src="star_off.gif"><td>
    <td><img src="star_off.gif"><td>
    <td><img src="star_off.gif"><td>
    ...
  <tr>
  </tr>
    <td><img src="star_off.gif"><td>
    <td><img src="star_off.gif"><td>
    <td><img src="star_off.gif"><td>
    ...
  <tr>
  ...
</table>
```

The goal of this lesson is to be able to mouse over the table and have the stars turn 'on' wherever the mouse goes using the 'mouseover' event (see demo). But instead of creating 100 event handlers, just create one handler on the table that uses the event's target property to change the src property of the correct star.

Solution:
``` javascript
var handler = function(e) {
  if (e.target.src) e.target.src = "star_on.gif";   
}
document.getElementById("star_table").addEventListener('mouseover', handler, false);
```

#### Exercise: Context menu

For this exercise we want to implement a custom context menu for Tux, the penguin.

	
This is the HTML for a menu which exists, but is currently hidden:

``` html
<div id="menu">
  <div id="option1">Photograph</div>
  <div id="option2">Rub belly</div>
  <div id="option3">Feed a fish</div>
</div>
```

Write some JavaScript code below that does as many of the following as you can:

1. Add a click event handler to the penguin (his id is "tux") that makes the menu visible (style.display = 'block').
2. Move the menu (e.g. style.left = '123px' and style.top = '123px') to the mouse's location. Use the event's pageX and pageY properties.
3. Instead of using click, use contextmenu to detect the right mouse button.
4. Supress the browser's own context menu.
5. Add a click handler to the whole page (document.body) that hides the menu (style.display = 'none').
6. Add event handlers to each option that does something.

Solution:
``` javascript
var menu = document.getElementById("menu");

document.getElementById("tux").addEventListener('contextmenu', function(e) {
  e.preventDefault();
  menu.style.left = e.pageX + 'px';
  menu.style.top = e.pageY + 'px';
  menu.style.display = 'block';
}, false);

document.body.addEventListener('click', function() {
  menu.style.display = 'none';
}, false);

document.getElementById("option1").addEventListener('click', function() {
  this.style.background = 'green';
}, false);

document.getElementById("option2").addEventListener('click', function() {
  this.style.fontStyle = 'italic';
}, false);

document.getElementById("option3").addEventListener('click', function() {
  this.style.fontFamily = 'Charcoal';
}, false);
```