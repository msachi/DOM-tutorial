## Tutorial 2: Manipulating the DOM

#### Exercise: Roller Coaster Text

You now know the API for manipulating a DOM tree. For this exercise, put all these pieces together to write code that takes a string and renders it with undulating font sizes. Each letter should be in its own 'span' tag, and each span's .style.fontSize property starts at '10px' and increases by 5 pixels until the middle of the string is reached, before shrinking back to 10 pixels.

Below is an empty div with the id 'rollercoaster' which you can append to.

Solution:
``` javascript
var text = 'abcdefghijklmn';
var div = document.getElementById('rollercoaster');
var size = 10;
for (var i=0; i<text.length; i++) {
  var span = document.createElement('SPAN');
  var letter = document.createTextNode(text[i]);
  span.appendChild(letter);
  div.appendChild(span); 
  if (i<text.length/2) size = size + 5*(i+1);
  else size = size - 5*(text.length-i);
  span.style.fontSize = size + 'px';
}
```

Bonus: Try creating an undulating sine wave or shifting colours.