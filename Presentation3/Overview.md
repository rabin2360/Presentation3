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
  createCanvas(640, 480);
  background(200);
  drawingContext.fillStyle = "red";
  drawingContext.strokeStyle = "blue";
  drawingContext.fillRect(width/2, height/2, 55, 55);
  drawingContext.strokeRect(width/2, height/2, 55, 55);
}
```

The functions like `fillStyle`, `fillRect`, `strokeStyle`, `strokeRect`, etc. are HTML5 canvas functionality. They are working in conjunction with the functionality provided by p5.js to render an image of a rectangle that is red in color with blue borders. The output of the code above looks like below:
![Picture](https://github.com/rabin2360/Presentation3/blob/master/Presentation3/DrawContextExampleSquare.png)

###p5.js: Understanding `draw()` function 
In the following code, the `draw()` function is called on a loop and gives the impression of an animation. For the following code,
```
var x = 0;
var y = 0;

function setup() {
  createCanvas(640, 480);
  y = height/2;
}

function draw() {
  background(200);
	y = y + random(-5, 5);
	
  if(x> width)
  {
	x = 0;
  }
  
  if(y > height || y < 0)
  {
	  y = 0;
  }
  
   noStroke();
   stroke(0);
   fill(51);
   ellipse(x, y, 30, 30);
   x = x+1;
}
```

the x-coordinate of the ellipse is constantly updated in a loop giving the impression that the ellipse is moving along the horizontal axis. However, the y-axis value of the ellipse is randomly incremented or decremented by a value from the range (-5, 5).
The setup gives an impression that the ellipse is moving in the horizontal direction and while doing so is bobbing up and down. All of this is achieved using the `draw()` method in p5.js. The above code results in an animation like below:

![Animated GIF](https://github.com/rabin2360/Presentation3/blob/master/Presentation3/Animation.gif)


###p5.js: Understanding mouse and touch interaction
In p5.js, a list of following methods are included to handle things like mouse and touch interaction with the user. This allow the program to respond to the interaction with the end user using mouse and touch pads. The following are some of the mouse and touch interactions
supported by p5.js
	* Mouse
		* mouseX: the system variable that tells the x-coordinate in relation to the (0,0) on the canvas.
		* mouseY:  the system variable that tells the y-coordinate in relation to the (0,0) on the canvas.
		* mouseIsPressed: the boolean system variable determines if the mouse is pressed or not.
		* mousePressed(): the function that gets called when the mouse button is pressed.
	* Touch
		* touchMoved(): the function is called everytime a touch move is registered.
		* touchStarted(): the function is called once after every time a touch is registered.
		* touchEnded(): the function is called every time a touch ends.


Following is the code that shows the use of `mousePressed()` function. In the following code, everytime the mouse is pressed within the canvas, that becomes the starting point for the drifting bubble. Also, everytime a mouse press is 
registered, the color of the bubble changes.
```
var x = 0;
var y = 0;
var r, g, b;

function setup() {
  createCanvas(640, 480);
  y = height/2;
  r = random(255);
  g = random(255);
  b = random(255);
}

function draw() {
  background(200);
	y = y + random(-5, 5);
	
  if(x> width)
  {
	x = 0;
  }
  
  if(y > height || y < 0)
  {
	  y = 0;
  }
  
   stroke(r, g, b);
   fill(r, g, b);
   ellipse(x, y, 30, 30);
   x = x+2;
   
}

function mousePressed()
{
	x = mouseX;
	y = mouseY;
	
	r = random(255);
	g = random(255);
	b = random(255);
}
```

On executing the code, the following behavior is observed
![Mouse Clicks](https://github.com/rabin2360/Presentation3/blob/master/Presentation3/MouseClicks.gif)
