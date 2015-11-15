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

### p5.js and WebGL:
p5.js works in conjunction with WebGL. p5.js uses two render modes: P2D (default renderer) and WebGL. In this section,
the workings of p5.js and WebGL will be discussed further. WebGL uses the HTML canvas to draw either the 2D or 3D rendering of
objects and shapes. 

### Enable WebGL:
To enable WebGL, in the function `createCanvas()`, a third parameter is introduced called `WEBGL`. The `setup()` function looks like
below:
```
	function setup()
	{
		createCanvas (windowWidth, windowHeight, WEBGL);
	}
```

When using WebGL, by default, the camera view is perspective with a 60 degree field of the view. The other options to override the default camera view are
perspective() and ortho(). Both of them have the following command structure
```
perspective(fovy, aspect, near, far);
ortho(left, right, bottom, top, near, far);
```

When using p5.js in the WebGL mode, the z-coordinate is introduced. The z-coordinate is the axis that is pointing away from the direction of the screen. For instance, if
the left hand index finger is pointing to the right and the middle finger is pointing downwards, the thumb will be pointing in the direction of the z-coordinate. The index finger
will be pointing in the direction of the x-coordinate and the middle finger will be pointing in the direction of y-coordinate.

Below is an example of creating a 3D box using WebGL with p5.js. The camera view used is perspective. 
```
function draw(){
  background(255);
  
  push();
  rotateX(PI/3);
  rotateZ(PI/3);
  box(80, 80, 80);
  pop();
  }
```

In the above code the box is rotated about the x-axis and the z-axis to give user the perspective that it's a 3D box. The box draw has the height, width and depth of 80. The `push()`
command saves the current drawing style settings and the transformations while and `pop()` commands restores the settings. Executing the above command, we get the following output:
![3D Box](https://github.com/rabin2360/Presentation3/blob/master/Presentation3/3DBox.png)

p5.js provides six different primitive geometry 3D shapes:
* box(): Command format `box(width, height, depth)`
* torus(): Command format `torus(torus_radius, tube_radius, [optional: number of segments])`
* cone(): Command format `cone(base_radius, height)`
* cylinder(): Command format `cylinder(base_radius, height, [optional: number of segments])`
* sphere(): Command format `sphere(raidus, [optional: number of segments])`
* plane(): Command format `plane(width, height)`

In addition to the 3D shapes, p5.js also supports 2D shapes like arc, ellipse, line, point, quad, rect and triangle.

Besides a set of primitive 2D and 3D shapes, p5.js also allows the user to define their own shapes. `beginShape()` and `endShape()` allow the user to define a set of vertices to define a shape as desired. The following code describes
a triangle defined using the aforementioned commands.
```
beginShape();
vertex(100,0,-100);
vertex(500,0,-50);
vertex(300,300,-100);
endShape();
```

On executing the code above, the following shape is observed in the browser.
![Custom Triangle](https://github.com/rabin2360/Presentation3/blob/master/Presentation3/CustomTriangle.png)

p5.js in conjunction with WebGL provides the following light functionality to render objects that look realistic:
* ambientLight()
* directionalLight()
* pointLight()

**Ambient Light**: The function `ambientLight()` creates an ambient light with a color. The syntax for it is

	`ambientLight(red, [optional: blue], [optional: green], [optional: opacity])`

In the following code, red ambient light is used on the cone that is 3D in shape and rotated about x, y and z axis. Following is the code to perform the action,
```
  background(255);
  
  push();
  rotateZ(frameCount * 0.01);
  rotateX(frameCount * 0.01);
  rotateY(frameCount * 0.01);
  ambientLight(255, 0, 0);
  cone(80,80);
  pop();
```

The code above when executed is displayed in the browser as follows:
![Ambient light cone](https://github.com/rabin2360/Presentation3/blob/master/Presentation3/AmbientLightCone.gif)

In the gif above, it can be seen that regardless of which angle the cone turns too, it is lit with the red ambient light consistently.

**Directional Light**: The function `directionalLight()` creates a directional light with color. As the name suggests, the light is shining from a certain direction at the object at display. The syntax for it is

```directionalLight(red, [optional: blue], [optional: green], [optional: opacity], x_axis, [optional: y_axis], [optional: z_axis])```

In the following code, blue light is used for directional lightning. Also, the cursor is the source of the directional light and as the position of the cursor changes, the direction of the light source also changes. 
```
function draw(){
  background(255);
  
  boxXValue = (mouseX/width - 0.5)*(10);
  boxYValue = (mouseY/height - 0.5)*(10);
  
  normalMaterial();
  
  push();
  directionalLight(0, 0, 255, 0, boxXValue, boxYValue, -1);
  sphere(100, 100);
  pop();
  }
``` 

On running the code above, the following behavior is observed:
![Directional light sphere](https://github.com/rabin2360/Presentation3/blob/master/Presentation3/DirectionalLightSphere.gif)

**Point Light**: The functoin `pointLight()` creates a point light with color. The syntax for it is

```pointLight(red, [optional: blue], [optional: green], [optional: opacity], x_axis, [optional: y_axis], [optional: z_axis])```

In the following code, red light is used for point lightning. The cursor is the source of the point light like the previous example. 
```
function draw(){
   
  background(255);
  
  boxXValue = (mouseX/width - 0.5)*(10);
  boxYValue = (mouseY/height - 0.5)*(10);
  
  normalMaterial();
  
  push();
  pointLight(255, 0, 0, 0, boxXValue, boxYValue, -1);
  sphere(100, 100);

  pop();
```

On running the code above, the following behavior is observed:
![Point light sphere](https://github.com/rabin2360/Presentation3/blob/master/Presentation3/PointLightSphere.gif)
