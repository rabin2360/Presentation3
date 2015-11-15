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

[Previous](https://github.com/rabin2360/Presentation3/blob/master/Overview.md)
