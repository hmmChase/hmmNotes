# **\_**Canvas**\_**

```
<canvas id="tutorial" width="150" height="150"></canvas>
```

- 2 attributes: height and width
  - When no width and height attributes are specified, the canvas will initially be 300 pixels wide and 150 pixels high
- The `<canvas>` element can be styled just like any normal image (margin, border, background…).

## **Fallback**

- insert the alternate content inside the `<canvas>` element.
- Browsers that don't support `<canvas>` will ignore the container and render the fallback content inside it
- Browsers that do support `<canvas>` will ignore the content inside the container

* Scripts can also check for support programmatically by simply testing for the presence of the `getContext()` method

```
var canvas = document.getElementById('tutorial');

if (canvas.getContext) {
    var ctx = canvas.getContext('2d');
    // drawing code here
} else {
    // canvas-unsupported code here
}
```

## **Rendering context**

- used to create and manipulate the content shown
- To display something, a script first needs to access the rendering context and draw on it

* `getContext()`
  - used to obtain the rendering context and its drawing functions
  - takes one parameter, the type of context
    - `var canvas = document.getElementById('tutorial');`
    - `var ctx = canvas.getContext('2d');`

## **Coordinate space**

- The default origin of the grid is positioned in the top left corner at coordinate (0,0).
- All elements are placed relative to the origin
- Normally 1 unit in the grid corresponds to 1 pixel on the canvas

## **\_**Shapes**\_**

### **Rectangles**

- only supports one primitive shape: rectangles

* There are three functions that draw rectangles on the canvas:
* fillRect(x, y, width, height) \* Draws a filled rectangle.
* strokeRect(x, y, width, height) \* Draws a rectangular outline.
* clearRect(x, y, width, height) \* Clears the specified rectangular area, making it fully transparent.

### **Paths**

- The only other primitive shapes are paths
- A path is a list of points, connected by segments of lines that can be of different shapes, curved or not, of different width and of different color
- paths are stored as a list of sub-paths (lines, arcs, etc) which together form a shape

* To make shapes using paths:
  - First, you create the path
    - beginPath()
      - Creates a new path. Once created, future drawing commands are directed into the path and used to build the path up.
      - Every time this method is called, the sub-path list is reset and we can start drawing new shapes.
  - Then you use drawing commands to draw into the path
    - https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D#Paths
  - Once the path has been created, you can stroke or fill the path to render it.
    - stroke()
      - Draws the shape by stroking its outline.
    - fill()
      - Draws a solid shape by filling the path's content area.
      - automatically closes any open shapes
  - An optional step, is to close the path
    - closePath()
      - tries to close the shape by drawing a straight line from the current point to the start

### **Moving the pen**

- moveTo(x, y)
  - Moves the pen to the coordinates specified by x and y.
  - like lifting a pen from one spot on a piece of paper and placing it on the next

### **Lines**

- lineTo(x, y)
  - Draws a line from the current drawing position to the position specified by x and y.

### **Arcs**

- arc(x, y, radius, startAngle, endAngle, anticlockwise)
  - Draws an arc which is centered at (x, y) position with radius r starting at startAngle and ending at endAngle going in the given direction indicated by anticlockwise (defaulting to clockwise).

* arcTo(x1, y1, x2, y2, radius)
  - Draws an arc with the given control points and radius, connected to the previous point by a straight line.

- Angles in the arc function are measured in radians, not degrees
  - To convert degrees to radians you can use the following JavaScript expression:
    - radians = (Math.PI/180)\*degrees

### **Bezier and quadratic curves**

- These are generally used to draw complex organic shapes.

* quadraticCurveTo(cp1x, cp1y, x, y)
  - Draws a quadratic Bézier curve from the current pen position to the end point specified by x and y, using the control point specified by cp1x and cp1y.
  - one control point

- bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)
  - Draws a cubic Bézier curve from the current pen position to the end point specified by x and y, using the control points specified by (cp1x, cp1y) and (cp2x, cp2y).
  - two control points

### **Rectangles**

- rect(x, y, width, height)
  - adds a rectangular path to a currently open path.
  - Draws a rectangle whose top-left corner is specified by (x, y) with the specified width and height.
  - When this method is executed, the current pen position is automatically reset to the default coordinates.

### **Path2D objects**

- caches or records drawing commands to play back your paths quickly

---

- Path2D()
  - This constructor returns a newly instantiated Path2D object, optionally with another path as an argument (creates a copy), or optionally with a string consisting of SVG path data.
- Path2D.addPath(path [, transform])
  - Adds a path to the current path with an optional transformation matrix.

### **SVG paths**

- var p = new Path2D('M10 10 h 80 v 80 h -80 Z');
- Another powerful feature of the new canvas Path2D API is using SVG path data to initialize paths on your canvas. This might allow you to pass around path data and re-use them in both, SVG and canvas.

## **\_**Styles and colors**\_**

### **Colors**

- fillStyle = color
  - Sets the style used when filling shapes.

* strokeStyle = color
  - Sets the style for shapes' outlines.

- When you set the strokeStyle and/or fillStyle property, the new value becomes the default for all shapes being drawn from then on

* the following examples describe the same color:

  - ctx.fillStyle = 'orange';
  - ctx.fillStyle = '#FFA500';
  - ctx.fillStyle = 'rgb(255, 165, 0)';
  - ctx.fillStyle = 'rgba(255, 165, 0, 1)';

* must specify color before drawing

### **Transparency**

- useful if you want to draw a lot of shapes on the canvas with similar transparency

* globalAlpha = transparencyValue
  - Applies the specified transparency value to all future shapes drawn on the canvas. The value must be between 0.0 (fully transparent) to 1.0 (fully opaque). This value is 1.0 (fully opaque) by default.

### **Line styles**

- There are several properties which allow us to style lines.

* lineWidth = value
  - Sets the width of lines drawn in the future.
* lineCap = type
  - Sets the appearance of the ends of lines.
* lineJoin = type
  - Sets the appearance of the "corners" where lines meet.
* miterLimit = value
  - Establishes a limit on the miter when two lines join at a sharp angle, to let you control how thick the junction becomes.
* getLineDash()
  - Returns the current line dash pattern array containing an even number of non-negative numbers.
* setLineDash(segments)
  - Sets the current line dash pattern.
* lineDashOffset = value
  - Specifies where to start a dash array on a line.

### **Gradients**

- create a CanvasGradient object to fill and stroke shapes using linear and radial gradients by using one of the following methods

* createLinearGradient(x1, y1, x2, y2)
  - Creates a linear gradient object with a starting point of (x1, y1) and an end point of (x2, y2).

- createRadialGradient(x1, y1, r1, x2, y2, r2)
  - Creates a radial gradient. The parameters represent two circles, one with its center at (x1, y1) and a radius of r1, and the other with its center at (x2, y2) with a radius of r2.

* gradient.addColorStop(position, color)
  - Creates a new color stop on the gradient object. The position is a number between 0.0 and 1.0 and defines the relative position of the color in the gradient, and the color argument must be a string representing a CSS <color>, indicating the color the gradient should reach at that offset into the transition.

### **Patterns**

- A simpler method than using a series of loops to create a pattern

* createPattern(image, type)
  - Creates and returns a new canvas pattern object. image is a CanvasImageSource (that is, an HTMLImageElement, another canvas, a <video> element, or the like. type is a string indicating how to use the image.

### **Shadows**

- shadowOffsetX = float
  - Indicates the horizontal distance the shadow should extend from the object. This value isn't affected by the transformation matrix. The default is 0.
- shadowOffsetY = float
  - Indicates the vertical distance the shadow should extend from the object. This value isn't affected by the transformation matrix. The default is 0.
- shadowBlur = float
  - Indicates the size of the blurring effect; this value doesn't correspond to a number of pixels and is not affected by the current transformation matrix. The default value is 0.
- shadowColor = color
  - A standard CSS color value indicating the color of the shadow effect; by default, it is fully-transparent black.

### **Canvas fill rules**

- you can optionally provide a fill rule algorithm by which to determine if a point is inside or outside a path and thus if it gets filled or not
- useful when a path intersects itself or is nested

* Two values are possible:
  - "nonzero": The non-zero winding rule, which is the default rule.
  - "evenodd": The even-odd winding rule.

## **\_**Text**\_**

### **Drawing text**

- fillText(text, x, y [, maxWidth])
  - Fills a given text at the given (x,y) position. Optionally with a maximum width to draw.

* strokeText(text, x, y [, maxWidth])
  - Strokes a given text at the given (x,y) position. Optionally with a maximum width to draw.

### **Styling text**

- font = value
  - The current text style being used when drawing text. This string uses the same syntax as the CSS font property. The default font is 10px sans-serif.
- textAlign = value
  - Text alignment setting. Possible values: start, end, left, right or center. The default value is start.
- textBaseline = value
  - Baseline alignment setting. Possible values: top, hanging, middle, alphabetic, ideographic, bottom. The default value is alphabetic.
- direction = value
  - Directionality. Possible values: ltr, rtl, inherit. The default value is inherit.

### **Advanced text measurements**

- measureText()
  - Returns a TextMetrics object containing the width, in pixels, that the specified text will be when drawn in the current text style.

## **\_**Images**\_**

### **Using images**

- Importing images into a canvas is basically a two-step process:
  - Get a reference to an HTMLImageElement object or to another canvas element as a source. It is also possible to use images by providing a URL.
  - Draw the image on the canvas using the drawImage() function.

### **Getting images to draw**

- The canvas API is able to use any of the following data types as an image source:
  - HTMLImageElement
    - These are images created using the Image() constructor, as well as any <img> element.
  - SVGImageElement
    - These are images embedded using the <image> element.
  - HTMLVideoElement
    - Using an HTML <video> element as your image source grabs the current frame from the video and uses it as an image.
  - HTMLCanvasElement
    - You can use another <canvas> element as your image source.
- These sources are collectively referred to by the type CanvasImageSource.

### **Ways to get images for use on a canvas**

- images from the same page
  - The document.images collection
  - The document.getElementsByTagName() method
  - If you know the ID of the specific image you wish to use, you can use document.getElementById() to retrieve that specific image

* images from other domains
  - Using the crossorigin attribute of an <img> element (reflected by the HTMLImageElement.crossOrigin property), you can request permission to load an image from another domain for use in your call to drawImage()

- using other canvas elements
  - Just as with normal images, we access other canvas elements using either the document.getElementsByTagName() or document.getElementById() method.

* creating an image from scratch
  - create new HTMLImageElement objects in our script. To do this, you can use the convenient Image() constructor
  - If you try to call drawImage() before the image has finished loading, it won't do anything

- embedding an image via data: URL
  - include images via the data: url

* using frames from a video
  - use frames from a video being presented by a <video> element

### **Drawing images**

- Once we have a reference to our source image object we can use the drawImage() method to render it to the canvas

* drawImage(image, x, y)
  - Draws the CanvasImageSource specified by the image parameter at the coordinates (x, y).
  - SVG images must specify a width and height in the root <svg> element.

### **Scaling**

- lets us place scaled images on the canvas.

* drawImage(image, x, y, width, height)
  - This adds the width and height parameters, which indicate the size to which to scale the image when drawing it onto the canvas.

### **Slicing**

- lets us cut out a section of the source image, then scale and draw it on our canvas

* drawImage(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight)
  - Given an image, this function takes the area of the source image specified by the rectangle whose top-left corner is (sx, sy) and whose width and height are sWidth and sHeight and draws it into the canvas, placing it on the canvas at (dx, dy) and scaling it to the size specified by dWidth and dHeight.

## **\_**Basic animations**\_**

- Steps to draw a frame:
  - Clear the canvas
    - Unless the shapes you'll be drawing fill the complete canvas (for instance a backdrop image), you need to clear any shapes that have been drawn previously. The easiest way to do this is using the clearRect() method.
  - Save the canvas state
    - If you're changing any setting (such as styles, transformations, etc.) which affect the canvas state and you want to make sure the original state is used each time a frame is drawn, you need to save that original state.
  - Draw animated shapes
    - The step where you do the actual frame rendering.
  - Restore the canvas state
    - If you've saved the state, restore it before drawing a new frame

### **Controlling an animation**

- Shapes are drawn to the canvas by using the canvas methods directly or by calling custom functions.
- In normal circumstances, we only see these results appear on the canvas when the script finishes executing.
- For instance, it isn't possible to do an animation from within a for loop.

### **Scheduled updates**

- used to call a specific function over a set period of time.

* setInterval(function, delay)
  - Starts repeatedly executing the function specified by function every delay milliseconds.
* setTimeout(function, delay)
  - Executes the function specified by function in delay milliseconds.
* requestAnimationFrame(callback)
  - Tells the browser that you wish to perform an animation and requests that the browser call a specified function to update an animation before the next repaint.
  - Repaints the window 60 times a second.

## _Collision detection_
