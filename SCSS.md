# _SCSS_

- https://sass-lang.com/

- Sass allows you to add more advanced syntax to your stylesheets
- SCSS is a version of Sass with syntax compatible with CSS
- A pre-processor is a tool that will process your code and compile it to a new format that adheres to the requirements of your environment

---

## Syntax

- Sass has two syntaxes
  - The `.sass` file extension uses the older syntax that is indentation-based and omits semicolons and curly brackets from the code
  - The newer and more widely used syntax belonging to the `.scss` file extension. It uses the standard CSS syntax with braces and semicolons.
- `&` - References parent selectors

---

## Variables

- Variables are defined by a `$` immediately preceding the name of the variable (like jQuery), and a colon separating the name of the variable from the value
- Should should be used when that value is need in multiple places

```
`// declare variable
$favorite-text-color: chartreuse;

// use in your stylesheet
p {
  color: $favorite-text-color;
}`
```

- Variables can be complex

```
$frilly-font: "Fantasy", cursive;
$main-font: "Arial", "Helvetica", "Copperplate", sans-serif;

$button-slide-transition: width 2s, height 2s, background-color 2s, transform 2s;

.main-content {
  font-family: $main-font;
  button {
    transition: $button-slide-transition;
  }
}
```

- Variables are easiest to change if they’re all located in the same stylesheet
- Create a file called `variables.scss` that houses all of your variables
- Then require said file in your other stylesheets using the syntax `@import "variables"`

---

## Nesting

- Nesting makes representing relationships between elements in HTML possible in CSS

```
`// target an anchor tag within a navigation element within a particular header tag

$main-text-dark: #000;
$red: #FF0000;
$link-light: #fff;

header {
  color: $main-text-dark;
  nav: {
    background-color: $dark-red;
    a { color: $link-light; }
  }
}`
```

- CSS output:

```
header { color: #000; }
header nav { background-color: #ff0000; }
header nav a { color: white; }
```

- Psuedo-Selectors/Elements should always be nested

```
`a {
  &:hover { color: pink; }
}`
```

---

## Color Functions

### RGBA

- Red, Green, Blue, Alpha(Opacity)
- Syntax: `rgba(0-255, 0-255, 0-255, 0-1)` or `rgba(0-100%, 0-100%, 0-100%, 0-1 )`
- Example: `rgba(255, 0, 0, 1)` or `rgba(100%, 0, 0, 1)` (red)

### Hexadecimal Code

- A form of RGB notation written as pairs of hexadecimal values
- Syntax: `#rrggbb` or `#rgb`
- Example: `#f00` or `#ff0000` (red)

### HSLA

- Hue, Saturation, Lightness, Alpha(Opacity)
- Syntax: `hsla(0-360, 0-100%, 0-100%, 0-1)`
- Example: `hsla(0, 100%, 50%, 1)` (red)

### complement(color)

- Returns the complement (aka the color that is 180 degrees from the value on the color wheel)
- Identical function to `adjust-hue(color, 180deg)`

### mix(color1, color2, weight)

- Mixes two given colors based on the weight percentage provided

### lighten/darken(color, amount)

- Takes a color and a percentage value, returning a color with a lightness increased or decreased by given amount.

### desaturate/saturate(color, amount)

- `desaturate()` will reduce a color’s saturation by that percentage
- `saturate()` will increase a color’s saturation by that percentage

---

## Math

- less useful due to flexbox and grid

---

## Mixins

- A mixin allows you to define a set of styles along with the option to pass in arguments that you can include in HTML elements, classes or IDs
- Mixins are great for reducing repetitive styles in your CSS

```
`// Example
@mixin border-radius($radius) {
  -webkit-border-radius: $radius;
     -moz-border-radius: $radius;
      -ms-border-radius: $radius;
          border-radius: $radius;
}

.box {
  @include border-radius(10px);
}`
```

---

## Functions

- A function returns a single value
- Does not include the CSS property

```
`@function make-pinker($value) {
  @return $value + rgb(100,0,0);
}

p {
    background: make-pinker(gray);
}`
```

---

## Extends

- Allows you to inherit properties from other classes and IDs
- Think of as parent styles – short, green eyes, big feet. Their children and grandchildren have the same base styles but with new age flair and coolness of their own.

```
`.message {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.success {
  @extend .message;
  border-color: green;
}`
```

---

## Control directives

### @if

- Returns any styles if the directive does not result in false or null

```
`// For debugging
@mixin debug-text($true) {
  @if $true {
    color: red;
  }
}

body {
  @include debug-text(true)
}

// Useful mixin using if and else statement
@mixin top-or-bottom($tb) {
  position: absolute;

  // Declare top or bottom
  @if $tb == top {
    top: 20px;
  }

  @else if $tb == bottom {
    bottom: 20px;
  }
}

.lower-text {
  @include top-or-bottom(bottom);
}`
```

### @each

- Loops through a list or map of variables
- This is handy in creating accurate class names with specific values

```
`@each $cohort in 1505, 1511, 1610, 1612 {
   .#{$cohort}-avatar {
       background-image: url('/img/#{$cohort}.png');
   }
}

$align-list: center, left, right;

@each $align in $align-list {
  .txt-#{$align} {
    text-align: $align;
  }
}`
```

### @for

- Output styles in a loop
- Uses a variable name to track the loop
- You can use from x through y to include the ending number or from x to y to not include it
- You can loop backwards by making the first number larger than the second

```
`@for $i from 1 through 12 {
  .col-#{$i} { width: 100/12 * $i;}
}`
```

### @while

- Output styles until the desired condition returns false.

```
`$z:1;

@while $z < 9 {
    .text-col-#{$z} {
      font-weight: 100 * $z;
    }
    $z: $z + 1;
};`
```

---

## Structure\*\* \*\*

- http://thesassway.com/beginner/how-to-structure-a-sass-project

---
