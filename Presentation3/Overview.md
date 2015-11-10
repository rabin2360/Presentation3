##p5.js: Overview
There are two main functions that p5 uses when an application is started:
	* `setup()`
	* `draw()`

`setup()`: The code in the `setup` function runs once. Typically, the code written in the `setup` block is used for initialization. It can also be used to create a progrom that does
not need looping repeatedly.
`draw()`: The draw block for the code runs in a constant loop. It is typically used for animation as it continues to run the block of code to give an impression that the code view is
dynamic and constantly changing.

For starters, let our JavaScript file contain the following code:
```
var x = 0;

function setup() {
  createCanvas(640, 480);
  background(100);
}

function draw() {
  ellipse(x, height/2, 20, 20);
  x = x+1;
}
```

###p5.js: Understanding `setup()` function
In the above code, the `setup()` function is creating a canvas that is of size 640 x 480. By default, if the `createCanvas` code is not included in the `setup()` method, the canvas drawn
will always be 100 x 100. Similarly, the `background()` method call in `setup()` method paints the background the canvas drawn. The canvas drawn is appeneded to the html page where the JavaScript
is rendered. The CSS styling present in the HTML page is affect where the canvas for p5.js is displayed. If the user wants to paint the canvas all over the screen, to override the default padding
provided by some of the browsers, the following styling code can be included in the HTML page.
```
<style> body{padding:0; margin:0;} </style>
```

In the HTML page, the user can also specify locations for the canvas to be drawn. In order to do that, a method call named `parent()` is used. In the body of the HTML file, the ID of the container
that will append the canvas can be defined. The container ID and the `parent()` call can be used the following way:

Definining the container ID:
```
<div id='ContainerToDisplayCanvas'></div>
``` 

Using the container ID in the `setup()` as follows:
```
function setup() {
  var canvas = createCanvas(640, 480);
  canvas.parent('ContainerToDisplayCanvas');
}
```

The p5.js also allows the user to work with the HTML5 Canvas functionality. The HTML5 canvas functionality can be accessed using `drawingContext`. For instance, in the following code

```
function setup() {
  drawingContext.shadowOffsetX = 5;
  drawingContext.shadowOffsetY = -5;
  drawingContext.shadowBlur = 10;
  drawingContext.shadowColor = "black";
  background(200);
  ellipse(width/2, height/2, 50, 50);
}
```

The functions like `shadowOffsetX`, `shadowOffsetY`, `shadowBlur`, `shadowColor`, etc. are HTML5 canvas functionality. They are working in conjunction with the functionality provided by 
p5.js. The output of the code above looks like below:
![Picture](https://github.com/rabin2360/Presentation3/tree/master/Presentation3/DrawContextExample.png)

###p5.js: Understanding `draw()` function 
In the following code, the `draw()` function is called on a loop and gives the impression of an animation. For the following code,
```
function draw() {
  ellipse(x, height/2, 20, 20);
  x = x+1;
}
```

the x-coordinate of the ellipse is constantly updated in a loop giving the impression that the ellipse is moving along the horizontal axis in a straight line. Usually, the setup for the animation being
performed is done in the `setup()` function and the actual animation is implemented in the `draw()` function.


