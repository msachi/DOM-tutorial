## Tutorial 4: Asynchronous Server Requests

#### Exercise: Collaborative Stars

The goal of this exercise is to write a collaborative drawing application where users can turn stars on and off and all other viewers of this page see the same pattern.

1. Add an event handler to each star (or to the table) so that when a star is clicked it toggles between on and off.
2. Send the clicked star's number (0-99) and new state (0 or 1) to the server in this format: /collab.py?n=99&s=1
3. The resulting response is a 100 character string that should be used to turn on or off each of the 100 stars.

Work through each step, one by one. When complete, you may wish to open another copy of this page in another window to verify that collaboration is occurring.

Here is a table containing 100 stars.

This is the HTML for the table to the left:

``` html
<table id="star_table">
  <tr>
    <td><img id="star_0" src="star_off.gif"><td>
    <td><img id="star_1" src="star_off.gif"><td>
    <td><img id="star_2" src="star_off.gif"><td>
    ...
  <tr>
  </tr>
    <td><img id="star_10" src="star_off.gif"><td>
    <td><img id="star_11" src="star_off.gif"><td>
    <td><img id="star_12" src="star_off.gif"><td>
    ...
  <tr>
  ...
</table>
```

Solution:
``` javascript
var table = document.getElementById('star_table');
var stars = table.getElementsByTagName('img');

var toggleStars = function(e) {
  if (e.target.src == "https://dom-tutorials.appspot.com/static/star_off.gif") e.target.src = "star_on.gif";
  else e.target.src = "star_off.gif";
  sendRequest(e);
};

var sendRequest = function(e) {
  var req = new XMLHttpRequest();
  var n = e.target.id.match(/\d+/);
  var s = +(/on/).test(e.target.src);
  req.open('GET', '/collab.py?n=' + n + '&s=' + s);
  req.onreadystatechange = updateStars;
  req.send();
};

var updateStars = function() { 
  if (this.readyState == 4 && this.status == 200) {
    var nums = this.responseText;
    for (var i=0; i<stars.length; i++) {
      nums[i] == 1 ? stars[i].src = "star_on.gif" : stars[i].src = "star_off.gif";
    }
  }
};

table.addEventListener('click', toggleStars, false);
```

Bonus #1: The 'GET' protocol should not be used to change server state, which is what is happening here. Convert the XMLHttpRequest to use 'POST'. See: Using POST method in XMLHttpRequest.

Bonus #2: Updates only happen when the user clicks a star. Try creating a recurring task with window.setInterval[?] that sends a request to /collab.py with no arguments to get an update.