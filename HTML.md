# _HTML_

---

**_Specs:_**

    * https://validator.w3.org/
    * https://validator.w3.org/checklink
    * https://platform.html5.org/
    * [www.caniuse.com](http://www.caniuse.com/)

**HTML**: provides the structure for content on a page

<!DOCTYPE html>
<html>
                <head>
                                <title></title>
                </head>
                <body>
                </body>
</html>


**_Document Object Model (DOM)_**

    * Relationship each element has with each other

**_Tags_**

    * things inside <>s are called tags. Tags are basic labels that define and separate parts of your markup into elements.

**Comments**: <!-- this syntax -->

**Meta:**

<!DOCTYPE> - tells the browser what version of HTML the page is written in
<head> - metadata
<title> - the title of the document
<meta> - provides information to search engines and browsers
<style> - define styles to apply to body elements
<link> - directive indicating related documents
<base> - defines the base address for all relative links on the page
<script> - defines a client-side script (JavaScript)
<style> - defines style information
<link> - defines a link between a document and an external resource

**Headings:**
<h1> - the main heading of a container
<h2-6> - use for semantic meaning

**Structural:**
<div> - generic block level container for grouping other elements

    * use when there is no semantic meaning to the container

<span> - generic inline level container for text and other inline elements

    * often used as a container for some text

<br /> - explicit line break

<hr /> - horizontal rule
<article> -
<aside> -
<header> -
<footer> -
<nav> -
<section> - a logical grouping of elements
<main> -

**Text:**
<p> - paragraphs
<pre> - whitespace is respected
<sup> - superscript, for notations
<sub> - subscript, for footnotes and references
<cite> - the title of a work
<address> - specifies such information as address, signature and authorship for the current document

    * typically placed at the top or bottom of the document
    * when used with %text, acts similar to a paragraph with breaks before and after

<abbr> - abbreviations
<acronym> - acronyms
<em> - emphasized text
<strong> - important text
<code> - code blocks
<samp> - samples
<kbd> - keyboard input
<var> - code variables

<blockquote> - block level quotes
<q> - inline level quotes

**Lists:**
<ul> - unordered list
<ol> - ordered list
<li> - list item
<dl> - definition list
<dt> - definition term
* * *

# _**Forms**_

- A form consists of any number of form fields grouped in a `<form>` tag
- Allows a user to fill out information and send it to the server

```
<form method="GET" action="example/message.html">
  <p>Name: <input type="text" name="name"></p>
  <p>Message:<br><textarea name="message"></textarea></p>
  <p><button type="submit">Send</button></p>
</form>
```

- When you click the Send button, the form is submitted
  - The content of its field is packed into an HTTP request and the browser navigates to the result of that request
- When the `<form>` element’s `method` attribute is `GET` (or is omitted), the information in the form is added to the end of the `action` URL as a query string
- The browser might make a request to this URL:

```
GET /example/message.html?name=Jean&message=Yes%3F HTTP/1.1
```

- If we change the `method` to `POST`, the HTTP request will put the query string in the body of the request, rather than adding it to the URL

```
POST /example/message.html HTTP/1.1
Content-length: 24
Content-type: application/x-www-form-urlencoded

name=Jean&message=Yes%3F
```

## Query Strings

- `GET /example/message.html?name=Jean&message=Yes%3F HTTP/1.1`
  - The question mark indicates the end of the path part of the URL and the start of the query
  - After that follow pairs of names and values, corresponding to the `name` attribute on the form field elements and the content of those elements, respectively
  - An ampersand character (`&`) is used to separate the pairs

## URL encoding

- A way to escape characters in a query string
- Uses a percent sign followed by two hexadecimal (base 16) digits that encode the character code
- In this case, 3F, which is 63 in decimal notation, is the code of a question mark character
- JavaScript provides the `encodeURIComponent` and `decodeURIComponent` functions to encode and decode this format

```
console.log(encodeURIComponent("Yes?"));
// → Yes%3F

console.log(decodeURIComponent("Yes%3F"));
// → Yes?
```

## Form Fields

- Form-associated content comprises elements that have a form owner, exposed by a form attribute
- A form owner is either the containing `<form>` element or the element whose id is specified in the form attribute

* When a field is contained in a `<form>` element, its DOM element will have a `form` property linking back to the form’s DOM element
* The `<form>` element, in turn, has a property called `elements` that contains an array-like collection of the fields inside it.
* The `name` attribute of a form field determines the way its value will be identified when the form is submitted
* It can also be used as a property name when accessing the form’s `elements` property, which acts both as an array-like object (accessible by number) and a map (accessible by name)

```
<form action="example/submit.html">
  Name: <input type="text" name="name"><br>
  Password: <input type="password" name="password"><br>
  <button type="submit">Log in</button>
</form>

<script>
  let form = document.querySelector("form");
  console.log(form.elements[1].type);
  // → password
  console.log(form.elements.password.type);
  // → password
  console.log(form.elements.name.form == form);
  // → true
</script>
```

- <button>
- <fieldset>
- <input>
    * The `type` attribute is used to select the field’s style
- <keygen>
- <label>
    * Associates a piece of document with an input field
    * Clicking anywhere on the label will activate the field, which focuses it and toggles its value when it is a checkbox or radio button
- <meter>
- <object>
- <output>
- <progress>
- <select>
    * Creates a field that allows the user to select from a number of predefined options
    * The `multiple` attribute allows the user to select any number of options
    * The `<option>` tags for a `<select>` field can be accessed as an array-like object through the field’s `options` property
- <option>
    * Provides the options for the `<select>` element
    * Has a property called `selected`, which indicates whether that option is currently selected
- <textarea>
    * Multi-line text fields

## Submitting

- A button with a `type` attribute of `submit` will, when pressed, cause the browser to navigate to the page indicated by the form’s `action` attribute
  - Pressing enter when a form field is focused has the same effect
- Before that happens, a `"submit"` event is fired
  - You can handle this event with JavaScript, and prevent this default behavior by calling `preventDefault` on the event object

```
<form action="example/submit.html">
  Value: <input type="text" name="value">
  <button type="submit">Save</button>
</form>

<script>
  let form = document.querySelector("form");
  form.addEventListener("submit", event => {
    console.log("Saving value", form.elements.value.value);
    event.preventDefault();
  });
</script>
```

- Intercepting `"submit"` events in JavaScript has various uses:
  - We can write code to verify that the values the user entered make sense and immediately show an error message instead of submitting the form
  - Or we can disable the regular way of submitting the form entirely, as in the example, and have our program handle the input, possibly using `fetch` to send it to a server without reloading the page

---

**Links:**
<a> - anchor – acts as either a source or target for linking

    * link representation is the content of the anchor tag
    * can link to sections of a page using named anchors (href=”#section” -> name=”section”)
    * can also use ID’s instead of named anchors

**Tables:**

    * used to represent data

<table> - the table
<caption> - table title
<thead> - header - single row (usually) for column headers
<tfoot> - footer - single row (usually) for totals, summary, etc.
<tbody> - body - multiple rows presenting data
<tr> - a row in the table

    * required in header, body, and footer

<th> - header data - defines a cell for data in the header
<td> - table data - defines a cell for data in the body or footer

**Media:**
<img> - images
<audio> -
<video> - videos
<object> - applications - flash, java, etc.
<canvas> - container to draw graphics, on the fly, via JavaScript
<svg> - a container for SVG graphics


?????
<bdi>
<datalist> -
<details> -
<embed> - host container for external plugins
<figcaption> -
<figuare> -
<input> - an input field where the user can enter data

    * used within a <form> element
    * the type attribute specifies the type of <input> element to display

<math> -
<mark> -
<meter> -
<output> - results of a calculation
<progress> -

<source> -
<summary> -
<time> -
<track> -
<wbr> -
<> -


**Self-closing tags:**

    * Optional
        * <html>, <head>, <body>, <p>, <dt>, <dd>, <li>, <option>, <thead>, <th>, <tbody>, <tr>, <td>, <tfoot>, <colgroup>
    * Strict
        * <img>, <input>, <br>, <hr>, <meta>

**_Character entities_**

    * &nbsp; - inserts a space which cannot be used for line breaks
    * &lt; &gt; - less-than and greater-than signs

**_Content categories_**
**\_** **\_**
**Metadata** - modify the presentation or the behavior of the rest of the document, set up links to other documents, or convey other out of band information

    * <base>, <command>, <link>, <meta>, <noscript>, <script>, <style>, <title>

**Flow** - typically contain text or embedded content

    * <a>, <abbr>, <address>, <article>, <aside>, <audio>, <b>,<bdo>, <bdi>, <blockquote>, <br>, <button>, <canvas>, <cite>, <code>, <command>, <data>, <datalist>, <del>, <details>, <dfn>, <div>, <dl>, <em>, <embed>, <fieldset>, <figure>, <footer>, <form>, <h1>, <h2>, <h3>, <h4>, <h5>, <h6>, <header>, <hgroup>, <hr>, <i>, <iframe>, <img>, <input>, <ins>, <kbd>, <keygen>, <label>, <main>, <map>, <mark>, <math>, <menu>, <meter>, <nav>, <noscript>, <object>, <ol>, <output>, <p>, <pre>, <progress>, <q>, <ruby>, <s>, <samp>, <script>, <section>, <select>, <small>, <span>, <strong>, <sub>, <sup>, <svg>, <table>, <template>, <textarea>, <time>, <ul>, <var>, <video>, <wbr>, Text

**Sectioning** - create a section in the current outline that defines the scope of <header> elements, <footer> elements, and heading content

    * <article>, <aside>, <nav>, <section>

**Heading** - defines the title of a section

    * <h1>, <h2>, <h3>, <h4>, <h5>, <h6>, <hgroup>

**Phrasing** - defines the text and the mark-up it contains. Runs of phrasing content make up paragraphs.

    * <abbr>, <audio>, <b>, <bdo>, <br>, <button>, <canvas>, <cite>, <code>, <command>, <data>, <datalist>, <dfn>, <em>, <embed>, <i>, <iframe>, <img>, <input>, <kbd>, <keygen>, <label>, <mark>, <math>, <meter>, <noscript>, <object>, <output>, <progress>, <q>, <ruby>, <samp>, <script>, <select>, <small>, <span>, <strong>, <sub>, <sup>, <svg>, <textarea>, <time>, <var>, <video>, <wbr>, and plain text



    * Some elements belong to this category only under specific conditions
        * <a>, <area>, <del>, <ins>, <link>, <map>, <meta>

**Embedded** - imports another resource or inserts content from another mark-up language or namespace into the document

    * <audio>, <canvas>, <embed>, <iframe>, <img>, <math>, <object>, <svg>, <video>

**Interactive** - elements that are specifically designed for user interaction

    * <a>, <button>, <details>, <embed>, <iframe>, <keygen>, <label>, <select>, <textarea>



    * Some elements belong to this category only under specific conditions:
        * <audio>, <img>, <input>, <menu>, <object>, <video>

**Palpable** - a content is palpable when it's neither empty nor hidden

**_User Input:_**

    * always replicate validation on the server

**Native Validation:**

    * value missing – *true* if an element marked as required has an empty value
    * type mismatch – *true* when the value is not matched to declared type
    * pattern mismatch – *true* when an elements value doesn’t match given regular expression
    * too long – *true* when an elements value length is longer than the value in the maxlength attribute
    * range underflow – *true* when a range types value is smaller than the min attribute
    * range overflow – *true* when a range types value is greater than the max attribute
    * step mismatch – *true* when a range type inputs value is impossible given the step value
    * valid – *true* when all other validation rules return false

**_Feature Detection:_**

    * [www.modernizr.com](http://www.modernizr.com/)
        * used to detect if a certain feature is supported by the user’s browser

**_Fallbacks & Polyfills:_**

    * [www.html5please.com](http://www.html5please.com/)

Fallbacks

    * provides a similar function for when a feature isn’t natively supported by the user’s browser

Polyfills

    * replicates the same interface and functionality as the native implementation

# **_Misc_**

---

**Children:** Every HTML element has a _parent_ element from which it _inherits_ properties.

**Semantics:** \*\*\*\*HTML is intended to describe the content it contains

    * the <span> and <div> elements are used where parts of a document cannot be semantically described by other HTML elements.

**Whitespace:**

    * inline elements are sensitive to the white space in your code



    * <p>
    *     <span>Foo</span>
    *     <span>Bar</span>
    * </p>
        * this code will produce a space equal to 1em between the two <spans>



    * <p>
    *     <span>Foo</span><span>Bar</span>
    * </p>
        * this code with not produce any spaces

** Attributes:**

- Should be written in kabob case

---

# **_Accessibility_**

## _WAI-ARIA_

- https://www.w3.org/TR/wai-aria/
- https://moritzgiessmann.de/accessibility-cheatsheet/
- https://www.udacity.com/course/web-accessibility--ud891
- https://developers.google.com/web/fundamentals/accessibility/semantics-aria/

* Accessible Rich Internet Applications\*\* \*\*

```
<p id="group1">Outer group</p>
<p id="item1">First item</p>
<div role="group" aria-labelledby="group1">
<a href="javascript:" role="button" aria-labelledby="item1">Item Content</a>
</div>
```

- Using `aria-labelledby`, VoiceOver will read the button as “First item Outer group button”. In other words, the button label, the group label and then the type of object

```
<p id="item1">First item</p>
<div role="group" aria-label="Outer group">
<a href="javascript:" role="button" aria-labelledby="item1">Item Content</a>
</div>
```

- Using `aria-label`, VoiceOver will now read the button as simple “First item button”
  - It doesn’t seem to matter which item uses `aria-label`, if it’s anywhere in the hierarchy, only the label for the button itself will be read out
- The `aria-label` attribute is used to define a string that labels the current element
  - Use it in cases where a text label is not visible on the screen
  - If there is visible text labeling the element, use `aria-labelledby` instead
- All inputs should have an `aria-label`
- Use semantic tags
- `Lang=”en”` attribute
- `alt` attributes on images
- Landmark roles
- Titles on links
- Tab index
- Forms around inputs
- Add accessibility to dynamic elements

* Roles
  - sets Landmarks
  - `role=”form”`
* States
  - `aria-checked=”true”`
  - `aria-expanded=”true”`
* Properties
  - Answers who am I related to?
  - `aria-controls`
  - `aria-label=”Name”`
  - `aria-labeledby=”element-id”`

---
