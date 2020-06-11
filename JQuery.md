# _JQuery_

- http://api.jquery.com/
- JQuery is a library of useful functions for JavaScript
- Allows us to use CSS selectors to find elements on the page and interact with them
- The syntax follows, “When I do _this_, make the CSS do _this_.”
  - Always starts with the dollar sign operator `$`
  - `$(".selector").function()`
- jQuery often selects an HTML/CSS element by using a selector, then does something to that element
- Query is zero-indexed, meaning that, counter-intuitively, `:odd` selects the second element, fourth element, and so on

---

# _Install_

- Insert before end of `<body>` tag and before JavaScript `<script>` import
- `<script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha256-3edrmyuQ0w65f8gfBsqowzjJe2iM6n0nKciPUp8y+7E=" crossorigin="anonymous"></script>`

---

# **_Methods_**

- `.ready()`
  - Loads scripts after HTML is rendered, to prevent bugs.

```
`$(document).ready(function() {`
`  // Your code here`
`});`
```

- `.toggleClass()`
  - Toggles something on and off

```
// When JQuery hears a click on the class .flash,
// it should add or remove the .laser class to or
// from anything with a .brain class.

$(".flash").click(function() {
  $(".brain").toggleClass('laser');
});

```

- `.addClass()`
  - Adds a class to an element

```
$("button").addClass("animated bounce");
```

- `.css()`
  - Changes the CSS of an element

```
$("body").css("background", randomRGBA);

$("#target1").css("color", "red");
```

- `.click()`
  - Binds an event handler to the "click" JavaScript event

```
$( "#target" ).click(function() {
  alert( "Handler for .click() called." );
});
```

- `.target()`
  - Use CSS Selectors to target elements
  - `.target:nth-child(n)` css selector allows you to select all the nth elements with the target class or element type

```
$(".target:nth-child(3)")
```

- `.html()`
  - Adds HTML tags and text within an element
  - Any content previously within the element will be completely replaced with the content you provide using this function

```
$("h3").html("<em>text</em>");

$(‘.prompt’).html(prompts[0]);
```

- `.val()`
  - Returns a value

* `.hide()`
  - Hides an element

- `.show()`
  - Shows an element

* `.remove()`
  - Removes an HTML element entirely

- `.prop()`
  - Adjusts the properties of elements

* `.text()`
  - Alters text without adding tags

- `.appendTo()`
  - Selects HTML elements and appends them to another element

* `.clone()`
  - Makes a copy of an element

- `.parent()`
  - Accesses the parent of whichever element you've selected

* `. children()`
  - Accesses the children of whichever element you've selected

---

# **Method Chaining**

- A technique that can be used to simplify code in scenarios that involve calling multiple functions on the same object consecutively.

* Without method chaining:

```
****var**** $div ****=**** $('#my-div');         **// assign to variable**

$div.css('background', 'blue');  **// set BG**
$div.height(100);                **// set height**
$div.fadeIn(200);                **// show element**
```

- With method chaining:

```
$('#my-div').css('background', 'blue').height(100).fadeIn(200);

**// often broken into multiple lines:**
$('#my-div')
  .css('background', 'blue')
  .height(100)
  .fadeIn(200);
```

---
