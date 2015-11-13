# Add-On Libraries 

p5.js is modular meaning that the developer only need use the p5.js features necessary for his/her project. [p5.js add-on libraries](http://p5js.org/libraries/#using-a-library) contain extra functionality in some cases useful for web development, such as p5.dom, and in other cases more education-oriented, such as p5.bots. 

Add-on libraries must be included in the project directory and linked to in the primary HTML file after p5.js.

```
<head>
  <script src="p5.js">
  <script src="p5.dom.js">
  <script src="sketch.js">
</head>
```

There are two types of libraries: core libraries that are part of the p5 distribution (currently p5.dom and p5.sound) and contributed libraries that are developed, owned, and maintained by members of the p5.js community.

## p5.dom

[p5.dom](http://p5js.org/reference/#/libraries/p5.dom) is a library that makes it possible to interact with other html objects.

The following code shows off some of the functionality of p5.dom.

```index.html``` is as simple as it possibly could be:

```
<html>
<head>
  <meta charset="UTF-8">
  <script language="javascript" type="text/javascript" src="../p5.js"></script>
  <script language="javascript" src="../addons/p5.dom.js"></script>
  <script language="javascript" type="text/javascript" src="sketch.js"></script>
  <style> body {padding: 0; margin: 0;} </style>
</head>
<body>
</body>
</html>
```

```sketch.js``` does all the work:

```
var slider;
function setup() {
  slider = createSlider(0, 255, 0);
  slider.position(10, 10);
  slider.style('width', '80px');
  slider.changed(addVal);
}

function draw() {
  var fillLevel = slider.value();
  if (fillLevel == 255) {
  	removeElements();
  }
  fill(fillLevel);
  ellipse(50, 75, 40, 40);
}

function addVal() {
	createDiv(slider.value());
}
```

1. Create a slider with parameters controlling its appearence, position, range, and initial value.
2. Add an event listener to the slider with the ```changed()``` function which will call the function included as its parameter every time the element it is attached to changes. In this case, the callback function ```addVal()``` simply adds a new div to the DOM containing the current position of the slider.
3. Create a new variable ```fillLevel`` to store the value of the slider.
4. If the fill level is equal to 255, remove all elements within the DOM including all added divs and the slider itself.
5. Otherwise, use the fill level to color an eclipse drawn in the canvas.

[p5.js have written a pretty substantial tutorial on using this add-on.](https://github.com/processing/p5.js/wiki/Beyond-the-canvas)

## p5.sound

## p5.play

## p5.particle

## p5.bots


