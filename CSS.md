# _CSS_

- https://css-tricks.com/almanac/
- https://www.w3.org/Style/CSS/Overview.en.html
- https://www.w3.org/TR/CSS/
- https://www.w3.org/TR/css-position-3/
- https://developer.mozilla.org/en-US/docs/Web/CSS

---

# **_Syntax_**

```
selector {
    property: value;
}
```

---

# **_Selectors_**

- **Class**
  - classifies elements
  - can be reused
  - use for all styling of elements
- **ID**
  - identifies elements
  - has to be unique and must appear only once per HTML document
  - only use ID’s as targets for JavaScript

* **`.class1#id1, .class1 #id1`**
  - The first part of the selector `.class1#id1` selects elements that contain both selectors
  - A comma separates multiple selectors that have the same styles
  - The last part `.class1 #id1` selects all elements with the id name `#id1` that are descendants (inside of) of the element with a class of `.class1`
* **`div ~ #id1`**
  - General Sibling Selector
  - Selects all elements with `#id1` that follow a `<div>`
  - Elements that follow one another are called siblings
  - They're on the same level/depth
* **`div + #id1`**
  - Adjacent Sibling Selector
  - Selects all elements with `#id1` that directly follow a `<div>`
* **`div > #id1`**
  - Child Selector
  - Selects all elements with `#id1` that are direct children of a `<div>`
  - A child element is any element that is nested directly in another element
  - Elements that are nested deeper than that are descendant elements
* **`*`**
  - Universal selector
  - Will select everything
* **`*, *:before, *:after`**
  - Makes pseudo elements use the same model, which otherwise wouldn't be selected by the `*` selector alone

---

# **_Pseudo-classes_**

- **`div:first-child`**
  - First Child Pseudo-selector
  - Selects all `<div>` elements that are the first child of an element
- **`div:last-child`**
  - Last Child Pseudo-selector
  - Selects all `<div>` elements that are the last child of an element
- **`div:only-child`**
  - Only Child Pseudo-selector
  - Selects all `<div>` elements that are the only child of an element
- **`div:nth-child(3)`**
  - Nth Child Pseudo-selector
  - Selects all `<div>` elements that are the Nth (ex: 3rd) child of an element
  - Can use `(odd)` and `(even)`
- **`div:nth-last-child(3)`**
  - Nth Last Child Pseudo-selector
  - Selects all `<div>` elements that are the Nth (ex: 3rd) child, counting from the bottom up, of an element
  - Can use `(odd)` and `(even)` and multiple values
- **`div:first-of-type`**
  - First of Type Pseudo-selector
  - Selects the first `<div>` in any element
- **`div:last-of-type`**
  - Last of Type Pseudo-selector
  - Selects the last `<div>` in any element
- **`div:nth-of-type(3)`**
  - Nth of Type Pseudo-selector
  - Selects all Nth (ex: 3rd) instances of a `<div>`
  - Can use `(odd)` and `(even)` and multiple values
- **`div:nth-of-type(6n+2)`**
  - Nth-of-type Pseudo-selector with Formula
  - Selects every 6th instance of a `<div>`, starting from (and including) the second instance
  - Can use `(odd)` and `(even)` and multiple values
- **`div:only-of-type`**
  - Only of Type Pseudo-selector
  - Selects a `<div>` within any element if it is the only `<div>` in there
- **`div:empty`**
  - Empty Pseudo-selector
  - Selects all empty `<div>` elements
- **`div:not(#id1)`**
  - Negation Pseudo-class
  - Selects all elements that do not have `id="id1"`
  - Can use `div:odd` and `div:even` and multiple values
  - Can you pseudo-selectors as a value
- `div:not(:first-child)`
  - Selects every div that is not a first child

---

# _Pseudo-elements_

- For every element on the page, you get two more free ones that you can do just about anything another HTML element could do
- Allows you to insert content onto a page from CSS
- The end result is not actually in the DOM
- Because you can absolutely position pseudo elements relative to their parent element, you can think of them as two extra layers to play with for every element
- Inline by default

* **`::before`**
  - Inserts the `content` before any other content in the HTML
* **`::after`**
  - Inserts the `content` after any other content in the HTML
* `**::hover**`

---

# **_Attribute selectors_**

- Targets a tag based on one of its attributes
- `input[type=text] {}`

---

# **_Box Model_**

- Content
  - blue
- Padding
  - Adjusts spacing within a container
  - green
- Border
  - Space between padding and margin
  - yellow
- Margin
  - Adjusts spacing between containers
  - red

---

# ----------

---

# **_display_**

- `**block**`
  - Structural elements
  - Container elements for grouping
  - Takes up the full width of the parent element
  - Adds line breaks before and after the element
  - Ignores the vertical-align property
  - Setting the width will prevent it from stretching out to the edges of its container

`<address>, <article>, <aside>, <blockquote>, <canvas>, <dd>, <div>, <dl>, <fieldset>, <figcaption>, <figure>, <footer>, <form>, <h1>, <h2>, <h3>, <h4>, <h5>, <h6>, <header>, <hgroup>, <hr>, <li>, <main>, <nav>, <noscript>, <ol>, <output>, <p>, <pre>, <section>, <table>, <tfoot>, <ul>, <video>`

- `**inline**`
  - Elements that flow like text
  - Does not create new lines
  - Can only contain data and other inline elements
  - Cannot take width, height, or top/bottom margins
  - Vertical padding will be ignored by other elements
  - Takes up only as much width as it needs
  - If floated left or right, will automatically become a block-level element
  - Subject to white-space settings
  - Subject to vertical-align property
  - Cannot put block elements inside inline elements, except for `<a>`
  - Respects whitespace in the markup
  - By default, an image sits on the same line that a, b, c and d sit on
    - There is space below that line for the descenders you find on letters like g, j, p and q. Block elements do not exhibit this

`<a>, <b>, <big>, <i>, <small>, <tt>, <abbr>, <acronym>, <cite>, <code>, <dfn>, <em>, <kbd>, <strong>, <samp>, <time>, <var>, <bdo>, <br>, <img>, <map>, <object>, <q>, <script>, <span>, <sub>, <sup>, <button>, <input>, <label>, <select>, <textarea>`

- `**inline-block**`
  - Makes the element a block box that flows like an inline box.
  - The main use of this value is when you want to give an inline element a width/height.
  - Can be used on a `<div>` to create a box that tightly wraps elements.
  - Can create a grid of boxes that fills the browser width and wraps nicely.
  - Elements are affected by the vertical-align property

* `**none**`
  - The element is not displayed at all
  - Will render the page as though the element does not exist

`<script>`

- `**flex**`
  - Elements behave like a block element and lays out its content according to the flexbox model
  - For one dimensional layouts (row or column)
  - Will expand

* `**grid**`
  - Elements behave like a block element and lays out its content according to the grid model
  - For two-dimensional layouts (rows and columns)
  - Grid areas can only be rectangles

- `**list-item**`
  - Elements generate a block box for the content and a separate list-item inline box

* `**table**`
  - Elements behave like `<table>` HTML elements. It defines a block-level box

- `**table-cell**`
  - Elements behave like `<td>` HTML elements

---

# **_position_**

- `**static**`
  - Default value
  - Elements follow the normal document flow
  - Not affected by `top`, `bottom`, `left`, `right`, and `z-index` properties

* `**relative**`
  - Tells the element to move relative to where it would have naturally landed
  - Behaves the same as a static, except it is now subject to the direction properties
  - Contents flow naturally into position
  - The positioning context is its original position
  - The space originally reserved for the element remains
  - Does not affect the position of other elements
  - If you apply both a left and right value, only the left value will be honored
  - The positional properties move the element away from the inside edge
  - Position using the direction properties of `top`, `right`, `bottom`, and `left`

- `**absolute**`
  - It’s positioned relative to the first parent element that is not `position: static`
  - If a positioned ancestor doesn't exist, it’s positioned relative to the browser viewport, i.e. the document body
  - Element is removed from the normal document flow
    - No space is created for the element in the page layout
    - Other elements will behave as if it’s not there
  - Can have margins, and they do not collapse with any other margins
  - It’s positioned away from the edge specified
  - If you apply both a left and right value, it will stretch the element to reach both of those values
  - Position using the direction properties of `top`, `right`, `bottom`, and `left`

* `**fixed**`
  - Anchors an element to the browser window
  - Same as absolute, with 2 exceptions:
    - the positioning context is always the viewport
    - element will not move when the document is scrolled
  - Respects margins
  - Position using the direction properties of `top`, `right`, `bottom`, and `left`

- `**sticky**`
  - A hybrid of `relative` and `fixed` positioning
  - Flows normally, and then is offset relative to its flow root and containing block
  - Treated as relatively positioned until it crosses a specified scroll threshold, at which point it is treated as fixed
  - The `top` property specifies the point where the element becomes sticky
  - Position using the direction properties of `top`, `right`, `bottom`, and `left`

---

# _Positioning_**_ values_**

- Used when position type is not `static`
- Moves an element relative to the positioning context

- Position absolute or fixed
  - Specifies the distance between the element's edge and the edge of its contextual containing block
  - Using a value of 0 will push the elements edge against the edge of the contextual containing block
- Position relative
  - Specifies the distance the element's edge is moved from its normal position
- Position sticky
  - Behaves like its position is relative when the element is inside the viewport, and like its position is fixed when it is outside

## top

- Y axis
- auto: default
- A negative value will move up

## right

## bottom

## left

- X axis
- ? a negative value will move right

---

# **_z-index_**

- Determines how elements are stacked on top of each other
- If you want something to go behind your main layer, give it a negative value
- If you want it in front, give it a number greater than zero
- The last element at the same hierarchy level appears on top

---

# **_float_**

- Removes elements from the normal document flow and pushes them to a specified edge
- Elements following a floated element will wrap around the floated element
  - Even other floated elements, unless `clear` is applied to them
- Floated elements become block boxes
- You should always set a width on floated items
  - Except if applied directly to an image, which has implicit width
- Floated elements stack up to the parent edge, then move down to next available edge
- The last floated item in the CSS will break first

* `**left**`
  - Element must float on the left side of its containing block
* `**right**`
  - Element must float on the right side of its containing block
* `**none**`
  - Default
  - The element does not float

---

# background

```
background:
  url(sweettexture.jpg)    /* image */
  top center / 200px 200px /* position / size */
  no-repeat                /* repeat */
  fixed                    /* attachment */
  padding-box              /* origin */
  content-box              /* clip */
  red                      /* color */
```

- **`background-clip`**
  - Specifies if an element's background extends underneath its border
  - `border-box`
    - The background extends to the outside edge of the border (but underneath the border in z-ordering)
  - `padding-box`
    - The background extends to the inside edge of the border
    - No background is drawn beneath the border
  - `content-box`
    - The background extends only to the edge of the content box
- **`background-color`**
  - Keyword values
    - `background-color: red`
  - Hexadecimal value
    - `background-color: #bbff00`
  - RGB value
    - `background-color: rgba(117, 190, 218, 0.5)`
  - HSL value
    - `background-color: hsla(50, 33%, 25%, 0.75)`
  - Special keyword values
    - `background-color: currentcolor`
    - `background-color: transparent`
- **`background-image`**
  - Applies a graphic or gradient to the background of an element
  - ` background``:`` ``url(sweettexture.jpg) `
  - ` background``:`` ``linear-gradient``(``black, white``) `
  - ` background``:`` ``radial-gradient``(``circle, black, white``) `
- **`background-origin`**
  - Similar to `background-clip`, except it resizes the background rather than clipping it
- **`background-position`**
  - Allows you to move a background around within its container
  - Has three different types of values
    - Length values
      - `100px 5px`
    - Percentages
      - `100% 5%`
    - Keywords
      - ` left | ``center | ``right | t``op | ``bottom `
  - 1 or 2 value syntax
    - `background-position: center`
    - `background-position: 25% 75%`
  - Edge offsets values
    - `background-position: bottom 10px right 20px`
- **`background-repeat`**
  - Defines how `background-images` are repeated
  - `repeat`
    - Default
    - Tile the image in both directions
  - `repeat-x`
    - Tile the image horizontally
  - `repeat-y`
    - Tile the image vertically
  - `space`
    - Tile the image in both directions
    - If multiple images can fit, space them out evenly, with images always touching the edges
  - `round`
    - Tile the image in both directions
    - If multiple images can fit with leftover space, squish them or stretch them to fill the space
  - `no-repeat`
    - Just show the image once
- **`background-size`**
  - `contain`
    - Scales the image as large as possible without cropping or stretching the image
  - `cover`
    - Scales the image as large as possible without stretching the image
    - It is cropped either vertically or horizontally so that no empty space remains
  - `auto`
    - Default
    - Scales the background image in the corresponding direction such that its intrinsic proportions are maintained
  - `<length>`
    - Stretches the image in the corresponding dimension to the specified length
  - `<percentage>`
    - Stretches the image in the corresponding dimension to the specified percentage of the background positioning area
- **`background-attachment`**
  - Determines whether the image's position is fixed within the viewport, or scrolls along with its containing block
  - `scroll`
    - Default
    - The background is fixed relative to the element itself and does not scroll with its contents
  - `fixed`
    - The background is fixed relative to the viewport
    - Even if an element has a scrolling mechanism, the background doesn't move with the element
  - `local`
    - The background is fixed relative to the element's contents
    - If the element has a scrolling mechanism, the background scrolls with the element's contents

---

# **_box-sizing_**

- **`content-box`**
  - Default
  - If you set an element's width to 100 pixels, then the element's content box will be 100 pixels wide, and the width of any border or padding will be added to the final rendered width
- `**border-box**`
  - Tells the browser to account for any border and padding in the value you specify for width and height
  - If you set an element's width to 100 pixels, that 100 pixels will include any border or padding you added, and the content box will shrink to absorb that extra width
  - Some experts recommend applying `box-sizing: border-box` to all elements

---

# **\_**clear**\_**

- Specifies whether an element should wrap around floated elements that precede it, or be moved down (cleared) below them
- Moves elements down below floated elements

* `**left**`
  - Will clear elements floated to the left
* `**right**`
  - Will clear elements floated to the right
* `**both**`
  - Will clear elements floated either left or right
* `**none**`
  - Default
  - Will not clear floats

## Clearfix

- The clearfix is a way to combat the zero-height container problem for floated elements
- Apply it to any parent element in which you need to clear the floats

```
.group::after {
  content: "";
  display: table;
  clear: both;
}
```

---

# **_columns_**

- extends the block layout mode to allow the easy definition of multiple columns of text
- columns are new, so you need to use prefixes
- content is automatically flowed from one column into the next as needed

## `columns`

- shorthand property allowing to set both the column-width and the column-count properties at the same time

## `column-width`

- specifies the minimum column width

## `column-count`

- describes the number of columns of the element

## `column-gap`

- sets the size of the gap between columns

---

# **_Flexbox_**

- https://css-tricks.com/snippets/css/a-guide-to-flexbox/
- An area of a document laid out using flexbox is called a flex container
- To create a flex container, we set the value of the area's container's `display` property to `flex` or `inline-flex`
- As soon as we do this the direct children of that container become flex items
- When creating a flex container all of the contained flex items will behave in the following way:
  - Items display in a row (the `flex-direction` property's default is `row`)
  - The items start from the start edge of the main axis
  - The items do not stretch on the main dimension, but can shrink
  - The items will stretch to fill the size of the cross axis
  - The `flex-basis` property is set to `auto`
  - The `flex-wrap` property is set to `nowrap`
- The result of this is that:
  - Items will all line up in a row, using the size of the content as their size in the main axis
  - If there are more items than can fit in the container, they will not wrap but will instead overflow
  - If some items are taller than others, all items will stretch along the cross axis to fill its full size

## _Parent properties (flex container)_

### flex-direction

- The direction items are placed in the container
- Establishes the main-axis
- `**row**` - Items are placed the same as the text direction (default)
- `**row-reverse**` - Items are placed opposite to the text direction
- `**column**` - Items are placed top to bottom
- `**column-reverse**` - Items are placed bottom to top

### flex-wrap

- Changes line wrapping behavior
- **`nowrap`** - All flex items will be on one line (default)
- **`wrap`** - Flex items will wrap onto multiple lines, from top to bottom
- **`wrap-reverse`** - Flex items will wrap onto multiple lines from bottom to top

### flex-flow

- Defines the flex container's main and cross-axis
  - Shorthand for `flex-direction` and `flex-wrap`
- `flex-flow: <‘flex-direction’> || <‘flex-wrap’>`

### justify-content

- Aligns flex items along main-axis (default horizontally)
  - Unless `flex-direction` is changed
- `**flex-start**` - Items align to the left side of the container (default)
- `**flex-end**`- Items align to the right side of the container
- `**center**` - Items align at the center of the container
- `**space-between**` - Items display with equal spacing between them
- `**space-around**` - Items display with equal spacing around them

### align-items

- Aligns flex items along cross-axis (default vertically)
  - Unless `flex-direction` is changed
- Requires the container to have a defined height (for default)
- `**stretch**` - Items are stretched to fit the container (default)
- `**flex-start**` - Items align to the top of the container
- `**flex-end**` - Items align to the bottom of the container
- `**center**` - Items align at the vertical center of the container
- `**baseline**` - Items display at the baseline (the bottom of text) of the container

### align-content

- Aligns a flex container's lines within when there is extra space in the cross-axis
- Similar to how `justify-content` aligns individual items within the main-axis
- Determines how to account for extra space in the cross-axis
- **`stretch`** - Lines stretch to take up the remaining space (default)
- **`flex-start`** - Lines packed to the start of the container
- **`flex-end`** - Lines packed to the end of the container
- **`center`** - Lines packed to the center of the container
- **`space-between`** - Lines evenly distributed; the first line is at the start of the container while the last one is at the end
- **`space-around`** - Lines evenly distributed with equal space around each line

## _Children properties (flex items)_

- `float`, `clear` and `vertical-align` have no effect on a flex item

### order

- Controls the order flex items appear in the flex container
- Default is 0 (source order)
- ` order``:`` <integer> `
- Assigning an order greater than 0 to an item will move it to the end of the items
- The largest `order` number will appear last, after the second largest, and so on

### flex-grow

- Dictates what amount of the available space inside the flex container the item should take up
- Default is 0
- ` flex-grow:`` <number> `
- `flex-grow: 1`
  - When applied to all items, evenly distributes available space on main-axis to all items
- `flex-grow: 2`
  - Will give an item twice the amount of evenly distributed space
- `flex-grow: 3`
  - 3 times
- Can use negative numbers
- Affects selecting text across items

### flex-shrink

- Defines the ability for a flex item to shrink space is limited
- Defines how much to reduce an items size relative to other items when there is not enough space based on `flex-basis`
- Default is 1
- ` flex-shrink``:`` <number> `

### flex-basis

- Defines the default size of an element before the remaining space is distributed
- The size is following `flex-direction` (`width` for `row`, `height` for `column`)
- Sets the size of an item before `flex-grow` and `flex-shrink` are factored
- Default is auto (uses width/height property)
- Length can be `%`, `em`, `rem`, or a keyword
  - If set to `0`, the extra space around content isn't factored in
  - If set to `auto`, the extra space is distributed based on its `flex-grow` value
  - Keywords: `content`, `min-content`, `max-content`, `fit-content`
- ` flex-basis``:`` <length> | auto `

### flex

- Shorthand for `flex-grow,` `flex-shrink` and `flex-basis`
  - `flex-shrink` and `flex-basis` are optional
- Default is `0 1 auto`
- `flex: 1` will set set `flex-grow` and `flex-shrink` to `1`
- \*\* \*\*Recommended instead of setting the individual properties
- ` flex``:`` none | [ <``'flex-grow'``> <``'flex-shrink'``>? || <``'flex-basis'``> ] `

### align-self

- Allows the default alignment (or the one specified by `align-items` to be overridden for individual flex items
- Values are the same as `align-items`
- ` align-self``:`` auto | flex-start | flex-end | center | baseline | stretch `

---

# _Grid_

- https://css-tricks.com/snippets/css/complete-guide-grid/
- Allows you to create a grid in an element and place items anywhere in that grid
- The parent element is referred to as the container and its children are called items
- The content of each item is located in a box which is referred to as a cell

* Elements that are assigned to the same cell will not have any flow applied
  - They will be positioned one over the other, as if they were absolutely positioned

## _Units_

- `fr` (fractional): sets the column or row to a fraction of the available space
- `auto`: sets the column or row to the width or height of its content automatically
- `%`: adjusts the column or row to the percent width of its container
- `span`:

## _Parent properties (grid container)_

### display

- Defines the element as a grid container and establishes a new grid formatting context for its contents
- `**grid**` - generates a block-level grid
- `**inline-grid**` - generates an inline-level grid

### grid-template-columns / grid-template-rows

- Defines the columns and rows (tracks) of the grid with a space-separated list of value
- The values represent the track size, and the space between them represents the grid line
- Will automatically create implicit rows if the explicit rows don't have enough space for all the items
- `**<track-size>**` - can be a length, a percentage, or a fraction of the free space in the grid (using the `fr` unit)
- `**<line-name>**` - an arbitrary name of your choosing
- Keywords:
  - `auto`
    - Will take up any available space
  - `repeat()`
    - Repeats the same size for the specified number of rows
    - Takes 2 args - number of times to repeat, and what size to repeat
      - `repeat(4, 1fr)` will make 4 equal width columns/row
  - `auto-fill`
    - Fills the row with as many columns as it can fit
    - Creates implicit columns whenever a new column can fit, because it's trying to fill the row with as many columns as it can
    - ` grid-template-columns``:`` ``repeat``(``auto-fill``,`` ``minmax``(``100``px``,`` ``1``fr``)``)``; `
  - `auto-fit`
    - Fits the currently available columns into the space by expanding them so that they take up any available space
    - The browser does that after filling that extra space with extra columns (as with `auto-fill`) and then collapsing the empty ones
    - ` grid-template-columns``:`` ``repeat``(``auto-fit``,`` ``minmax``(``100``px``,`` ``1``fr``)``)``; `
  - `minmax`
    - Sets the minimum and maximum width for columns
    - The min can't be `fr`
    - ` grid-template-columns``:`` ``repeat``(``12``,`` ``minmax``(10rem``,`` ``1``fr``)``)``; `
  - `fit-content()`
    - Takes a clamp value
    - Creates a max width/height for an item
    - `fit-content(100px)`

### grid-template-areas

- Gives names to areas of the grid
- Defines a grid template by referencing the names of the grid areas which are specified with the `grid-area` property
- `**<grid-area-name>**` - the name of a grid area specified with `grid-area`
- `**.**` - a period signifies an empty grid cell
- `**none**` - no grid areas are defined

### grid-template

- A shorthand for setting `grid-template-rows`, `grid-template-columns`, and `grid-template-areas` in a single declaration
- `**none**` - sets all three properties to their initial values
- **`<grid-template-rows>` / `<grid-template-columns>`** - sets `grid-template-columns` and `grid-template-rows` to the specified values, respectively, and sets `grid-template-areas` to `none`

### grid-column-gap / grid-row-gap

- Specifies the size of the grid lines
- Works like margin for tracks
- `**<line-size>**` - a length value

### grid-gap

- A shorthand for `grid-row-gap` and `grid-column-gap`
- **`<grid-row-gap>` `<grid-column-gap>`** - length values

### justify-items

- Aligns grid items along the inline (row) axis
  - As opposed to `align-items` which aligns along the block (column) axis
- `**start**` - aligns items to be flush with the start edge of their cell
- `**end**` - aligns items to be flush with the end edge of their cell
- `**center**` - aligns items in the center of their cell
- `**stretch**` - fills the whole width of the cell (this is the default)

### align-items

- Aligns grid items along the block (column) axis
  - As opposed to `justify-items` which aligns along the inline (row) axis
- `**start**` - aligns items to be flush with the start edge of their cell
- `**end**` - aligns items to be flush with the end edge of their cell
- `**center**` - aligns items in the center of their cell
- `**stretch**` - fills the whole height of the cell (this is the default)

### place-items

- Sets both the `align-items` and `justify-items` properties in a single declaration
- **`<align-items>` / `<justify-items>`** - The first value sets `align-items`, the second value `justify-items`
  - If the second value is omitted, the first value is assigned to both properties

### justify-content

- Sets the alignment of the grid within the grid container along the inline (row) axis
- `**start**` - aligns the grid to be flush with the start edge of the grid container
- `**end**` - aligns the grid to be flush with the end edge of the grid container
- `**center**` - aligns the grid in the center of the grid container
- `**stretch**` - resizes the grid items to allow the grid to fill the full width of the grid container
- `**space-around**` - places an even amount of space between each grid item, with half-sized spaces on the far ends
- `**space-between**` - places an even amount of space between each grid item, with no space at the far ends
- `**space-evenly**` - places an even amount of space between each grid item, including the far ends

### align-content

- Sets the alignment of the grid within the grid container along the block (column) axis
- `**start**` - aligns the grid to be flush with the start edge of the grid container
- `**end**` - aligns the grid to be flush with the end edge of the grid container
- `**center**` - aligns the grid in the center of the grid container
- `**stretch**` - resizes the grid items to allow the grid to fill the full height of the grid container
- `**space-around**` - places an even amount of space between each grid item, with half-sized spaces on the far ends
- `**space-between**` - places an even amount of space between each grid item, with no space at the far ends
- `**space-evenly**` - places an even amount of space between each grid item, including the far ends

### place-content

- Sets both the `align-content` and `justify-content` properties in a single declaration
- **`<align-content>` / `<justify-content>`** - The first value sets `align-content`, the second value `justify-content`
  - If the second value is omitted, the first value is assigned to both properties

### grid-auto-columns / grid-auto-rows

- Specifies the size of any auto-generated grid tracks (implicit grid tracks)
- Implicit tracks get created when there are more grid items than cells in the grid or when a grid item is placed outside of the explicit grid
- `**<track-size>**` - can be a length, a percentage, or a fraction of the free space in the grid (using the `fr` unit)

### grid-auto-flow

- If you have grid items that you don't explicitly place on the grid, the auto-placement algorithm kicks in to automatically place the items
- This property controls how the auto-placement algorithm works
- `**row**` - tells the auto-placement algorithm to fill in each row in turn, adding new rows as necessary (default)
- `**column**` - tells the auto-placement algorithm to fill in each column in turn, adding new columns as necessary
- `**dense**` - tells the auto-placement algorithm to attempt to fill in holes earlier in the grid if smaller items come up later

### grid

- A shorthand for setting all of the following properties in a single declaration:
  - `grid-template-rows`
  - `grid-template-columns`
  - `grid-template-areas`
  - `grid-auto-rows`
  - `grid-auto-columns`
  - `grid-auto-flow`
- `**none**` - sets all sub-properties to their initial values
- `**<grid-template>**` - works the same as the `grid-template` shorthand
- **`<grid-template-rows>` / [ auto-flow && dense? ] `<grid-auto-columns>`?** - sets `grid-template-rows` to the specified value
  - If the `auto-flow` keyword is to the right of the slash, it sets `grid-auto-flow` to `column`
  - If the `dense` keyword is specified additionally, the auto-placement algorithm uses a “dense” packing algorithm
  - If `grid-auto-columns` is omitted, it is set to `auto`
- **[ auto-flow && dense? ] `<grid-auto-rows>`? / `<grid-template-columns>`** - sets `grid-template-columns` to the specified value
  - If the `auto-flow` keyword is to the left of the slash, it sets `grid-auto-flow` to `row`
  - If the `dense` keyword is specified additionally, the auto-placement algorithm uses a “dense” packing algorithm
  - If `grid-auto-rows` is omitted, it is set to `auto`

## _Children properties (grid items)_

### grid-column-start / grid-column-end / grid-row-start / grid-row-end

- Determines a grid item's location within the grid by referring to specific grid lines
- `grid-column-start`/`grid-row-start` is the line where the item begins
- `grid-column-end`/`grid-row-end` is the line where the item ends
- `**<line>**` - can be a number to refer to a numbered grid line, or a name to refer to a named grid line
- `**span <number>**` - the item will span across the provided number of grid tracks
- `**span <name>**` - the item will span across until it hits the next line with the provided name
- `**auto**` - indicates auto-placement, an automatic span, or a default span of one

### grid-column / grid-row

- Shorthand for `grid-column-start` + `grid-column-end`, and `grid-row-start` + `grid-row-end`, respectively
- `-1` will span to the end of the explicit track
- `**<start-line> / <end-line>**` - each one accepts all the same values as the longhand version, including span

### grid-area

- Gives an item a name so that it can be referenced by a template created with the `grid-template-areas` property
- Alternatively, this property can be used as an even shorter shorthand for `grid-row-start` + `grid-column-start` + `grid-row-end` + `grid-column-end`
- `grid-area:` horizontal line to start at `/` vertical line to start at `/` horizontal line to end at `/` vertical line to end at`;`
- `**<name>**` - a name of your choosing
- **`<row-start>` / `<column-start>` / `<row-end>` / `<column-end>`** - can be numbers or named lines

### justify-self

- Aligns a grid item inside a cell along the inline (row) axis
  - as opposed to `align-self` which aligns along the block (column) axis
- This value applies to a grid item inside a single cell
- `**start**` - aligns the grid item to be flush with the start edge of the cell
- `**end**` - aligns the grid item to be flush with the end edge of the cell
- `**center**` - aligns the grid item in the center of the cell
- `**stretch**` - fills the whole width of the cell (this is the default)

### align-self

- Aligns a grid item inside a cell along the block (column) axis
  - as opposed to `justify-self` which aligns along the inline (row) axis
- This value applies to the content inside a single grid item
- `**start**` - aligns the grid item to be flush with the start edge of the cell
- `**end**` - aligns the grid item to be flush with the end edge of the cell
- `**center**` - aligns the grid item in the center of the cell
- `**stretch**` - fills the whole height of the cell (this is the default)

### place-self

- Sets both the `align-self` and `justify-self` properties in a single declaration
- `**auto**` - The “default” alignment for the layout mode.
- **`<align-self>` / `<justify-self>`** - The first value sets `align-self`, the second value `justify-self`
  - If the second value is omitted, the first value is assigned to both properties

---

# **_overflow_**

- ` div ``{``overflow``:`` visible | hidden | scroll | auto | inherit ``} `
- Specifies whether to clip content, show scrollbars, or display overflowing content when it is too large for its block-level container
- Specifies what to do when an element's content is too large to fit in its block formatting context

* **`visible`**
  - Default
  - Content is not clipped when it proceeds outside its box
  - Specifying a value other than `visible` creates a new block formatting context
* **`hidden`**
  - Overflowing content will be hidden
* **`scroll`**
  - Similar to hidden except users will be able to scroll through the hidden content
* **`auto`**
  - If the content proceeds outside its box then that content will be hidden whilst a scroll bar should be visible for users to read the rest of the content
* **`initial`**
  - Uses the default value which is `visible`
* **`inherit`**
  - Sets the overflow to the value of its parent element

---

# _**text-align**_

- Specifies how inline or inline-block content is aligned in its parent block element
- Specifies how inline contents of a block are horizontally aligned, if the contents do not completely fill the line box
- Only applies to block elements

---

# _**vertical-align**_

- Specifies the vertical alignment of an inline, inline-block, and table box

---

# _**font-weight**_

- Sets the thickness of a font

---

# _**font-size**_

- Specifies the size of the font
- Affects not only the font to which it is applied, but is also used to compute the value of em, rem, and ex length units

---

# _content_

- Can only be used with the pseudo elements `:before` and `:after`
- The value for content can be:
  - A string
    - `content: "a string"`
    - special characters need to be specially encoded as a unicode entity
  - An image
    - `content: url(/path/to/image.jpg)`
    - The image is inserted at it's exact dimensions and cannot be resized
    - Since things like gradients are actually images, a pseudo element can be a gradient
  - Nothing
    - `content: ""`
    - Useful for clearfix and inserting images as background-images
    - Can set width and height, and can even resize with background-size
  - A counter
    - `content: counter(li)`
    - Really useful for styling lists until :marker comes along

---

# **_cursor_**

---

# _**outline**_

---

# _**border**_

## `**border-radius**`

- Can be used to shape `<div>`s

---

# _perspective_

- Gives an element a 3D-space by affecting the distance between the Z plane and the user
- The smaller the value, the closer you get from the Z plane and the more impressive the visual effect
- The greater the value, the more subtle will be the effect
- Setting perspective on the parent make all children share the same 3D-space and thus the same vanishing point
- Will skew a child element's `transform` property

---

# **_transition_**

- Ex. fades

---

# **_transform_**

- Allows you to visually manipulate an element by skewing, rotating, translating, or scaling
- All transforms for an element get listed together in the same declaration
- Ex. change colors

## rotate

- Use to rotate an element

## scaleY

- Finds the center of an element and flips it along the Y axis

---

# **_Animation_**

## **Keyframing**

- Use for multiple transformation
- Creates each step of the animation
- `@keyframes`

  - controls the intermediate steps in a CSS animation sequence by defining styles for keyframes (or waypoints) along the animation sequence
  - animation is created by gradually changing from one set of CSS styles to another
  - `0%` is the beginning of the animation, `100%` is when the animation is complete

- Define it
  - the property you want to change of the element you’re animating

```
@keyframes blink {
  50% {
    background: radial-gradient(circle, red 15%, transparent 40%), #cc5;
  }
}
```

- Assign it
  - assign the animation to the element

```
.element {
  animation: blink .5s infinite;
}
```

---

# **_Media Queries_**

- `@media`
  - modifies CSS based on the size of the device it is being shown on
- `@media only screen and (max-width: 600px) {...}`
  - If [device width] is less than or equal to 600px, then do {...}
- `@media only screen and (min-width: 600px) {...}`
  - If [device width] is greater than or equal to 600px, then do {...}
- `@media only screen and (max-width: 600px) and (min-width: 400px) {...}`
  - Will trigger only for screens that are 600-400px wide
- Common breakpoints
  - 600px, 900px, 1200px, and 1800px

---

# **_Sizing_**

## **%**

- a size relative to the containing block
- Relative to it’s parent properties
- When the parent’s height is determined by it’s children, there’s no known height to base % on, so the height is ignored entirely
- ? % widths won’t respect the min/max widths of other elements

## Fonts

- em
  - 1 em is equal to the default font size on whatever screen the user is using
- rem

## Blocks

- `min-height`
  - prevents the [used value](https://developer.mozilla.org/en-US/docs/Web/CSS/used_value) of the [`height`](https://developer.mozilla.org/en-US/docs/Web/CSS/height) property from becoming smaller than the value specified for `min-height`

## Viewport units

- The viewport is the area where the browser renders the site

- `vw`: 1/100th viewport width
- `vh`: 1/100th viewport height
- `vmin`: 1/100th of the smallest side
- `vmax`: 1/100th of the largest side

---

# **_Centering_**

## **Block tags**

- Fixed-width
  - set the margins to auto, which the remaining space will be split evenly between the two margins
- Set the `text-align` of the children to center

## **inline tags**

- Set tag to `display: block` and center using `margin: auto`
- Can’t be centered with `margin: auto`
- ? Can’t be centered with `text-align: center`

---

# **_Misc_**

## **_Vendor Prefixes_**

- `-webkit-` is for chrome
- `-moz-` is for mozilla

## **_Cascading_**

- CSS cascades down from the outermost containers to the inner ones.

## **\_**Specificity**\_**

- How the browser decides which CSS values are the most relevant to an element and whether or not they should be used
- Determines which CSS rules take precedence
- Specificity Calculator - [_https://specificity.keegan.st/_](https://specificity.keegan.st/)

## **_Stacking context_**

- HTML elements occupy this space in priority order based on element attributes
- A stacking context is formed, anywhere in the document, by any element in the following scenarios:
  - https://developer.mozilla.org/en/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context#The_stacking_context

## **_Positioning context_**

- When using a position property, the context is the element that the positioned element moves relative to

## **_Block formatting context_**

- https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Block_formatting_context
- The region in which the layout of block boxes occurs and in which floats interact with each other
- Contains everything inside of the element creating it that is not also inside a descendant element that creates a new block formatting context

## **_Ancestor element_**

- A structurally superior element, such as a parent element, or the parent of a parent element, and so on

## **_@import_**

- tells the CSS engine to include an external style sheet

## **_@page_**

- used to modify some CSS properties when printing a document
- can only change margins, orphans, widows, and page breaks

## **_Link to a stylesheet_**

- `<link type="text/css" rel="stylesheet" href="stylesheet.css"/>`

## **_Comments_**

- `/* this syntax */`

## **_Cascade Order_**

- Non-conflicting properties will be combined

## **_Margin collapsing_**

- when top and bottom margins come in contact with one another, if one margin is equal or greater than the other, then that margin overrides the other, leaving one margin
- if one margin is negative, the negative margin is subtracted from the positive margin, reducing the total vertical margin
- when all margins are negative, the size of the collapsed margin is the smallest (most negative) margin
- margins of floating and absolutely positioned elements never collapse
- use bottom margins as much as possible and avoid using top margins to avoid collapsing

## _Other_

- `!important`
  - prevents the overriding of a property by latter rules
- `white-space: nowrap;`
  - to prevent a row of inline boxes or text from wrapping to the next line
- `visibility: hidden;`
  - hides the element, but the element will still take up the space it would if it was fully visible
- **max-width**: limit how wide an element can be
- **min-width**: limit how thin an element can be
- **max-height**: limit how tall an element can be
- **min-height**: limit how short an element can be
  - use instead of width/height to improve the browser's handling of elements for mobile
- **<header>, <footer>**
  - If you use a fixed header/footer, make sure there is room for it by putting a margin top/bottom on the body
- `* + *`
  - Will apply a top margin to elements that follow an element

```
* + * {
  margin-top: 1rem;
}

const Box = styled.div`
  display: flex;
  flex-direction: vertical;
  > * + * {
    margin-top: 1rem;
}
```

---

# **_Organizing CSS properties_**

## **Idiomatic**

```
/* Positioning */
position: absolute;
z-index: 10;
top: 0;
right: 0;

/* Display & Box Model */
display: inline-block;
overflow: hidden;
box-sizing: border-box;
width: 100px;
height: 100px;
padding: 10px;
border: 10px solid #333;
margin: 10px;

/* Color */
background: #000;
color: #fff

/* Text */
font-family: sans-serif;
font-size: 16px;
line-height: 1.4;
text-align: right;

/* Other */
cursor: pointer;
```

---

# **_JavaScript_**

- Describe the style in CSS and then apply the class
  - `elem.className` corresponds to the "class" attribute
  - `elem.classList` is a special object with methods to add/remove/toggle classes
    - `elem.classList.add/remove("class")`
      - adds/removes the class
    - `elem.classList.toggle("class")`
      - if the class exists, then removes it, otherwise adds it
    - `elem.classList.contains("class")`
      - checks for the given class and returns true/false,
- We should only manipulate the style property if classes “can’t handle it”
  - `elem.style` is an object that corresponds to what’s written in the "style" attribute
    - `background-color = elem.style.backgroundColor`
- Resetting the style property
  - to hide an element, we can set `elem.style.display = "none"`
    - Then later we may want to remove the `style.display` as if it were not set
    - Instead of `delete elem.style.display` we should assign an empty line to it
      - `elem.style.display = ""`
- `style.cssText`
  - corresponds to the whole "style" attribute, the full string of styles
- `div.setAttribute`
- `getComputedStyle(element[, pseudo])`
  - returns the resolved value of the property

---

# _BEM_

- Block Element Modifier
- block\_\_element--modifier
- Naming
  - Blocks
    - must be unique
    - should equal CSS class
  - Elements
    - must be unique to the block
- No id's

---

# _Boilerplate_

```
/* * {
  margin: 0;
  padding: 0;
} */

*,
*::before,
*::after {
  box-sizing: border-box;
}

html {
  height: 100%;
}

body {
  min-height: 100%;
}
```

---

# **_Reset_**

- Browsers have a default stylesheet for when no custom styles are set
- Set padding, border, and margin to 0 to create a baseline

```
html, body, h1, h2, h3, h4, ul, ol, li, p, a {
    padding: 0;
    border: 0;
    margin: 0;
    font: inherit;
    font-size: 100%;
}
```

---

# _Frameworks_

## Tachyons

- http://tachyons.io/

## SPECTRE

- https://picturepan2.github.io/spectre/

---

# _Normalizers_

- nomalize.css
  - `npm install normalize.css`

* sanitize.css
  - `npm install sanitize.css`

- if installed as a package:
  - https://stackoverflow.com/questions/42119878/how-to-use-normalize-css-using-npm-install-with-webpack
  - in `index.js`
    - `import 'normalize.css/normalize.css';`
    - `import '`sanitize`.css/`sanitize`.css';`

* if included as a file
  - put in `/src/` folder
  - in `index.js`
    - `import './normalize.css';`
    - `import './sanitize.css';`

- using `@import`
  - in `index.css`
    - ` @import './``normalize.css'; `
      - as file
    - `@import '../node_modules/normalize.css/normalize.css';`
      - as package


        * `@import './sanitize.css';`
            * as file
        * `@import '../node_modules/sanitize.css/sanitize.css';`
            * as package

---

# _Misc_

## PurgeCSS

- Remove unused css
- https://github.com/FullHuman/purgecss

## DropCSS

- An exceptionally fast, thorough and tiny unused-CSS cleaner
- https://github.com/leeoniya/dropcss

---
