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

##p5.js: Understanding `setup()` function:
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

