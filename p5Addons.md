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

[p5.dom](http://p5js.org/reference/#/libraries/p5.dom) is a library that makes it possible to interact with other html objects. With p5.dom, developers can add, remove, and alter elements like text, sliders buttons, and images from the dom, track changes from dom elements and have those changes alter p5.js graphics, and control playback and parameters of media files.

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

[p5.sound, the second core library,](http://p5js.org/reference/#/libraries/p5.sound) is a powerful audio environment capable of sound synthesis, sound analysis, playback of pre-recorded audio, and real-time audio recorded from the computer's microphone (not supported by all browsers). p5.sound allows the developer to compose musical sequences ([that may respond to the user's manipulation of elements within the DOM.](http://b2renger.github.io/pages_p5js/springs/index.html))

The following example illustrates a few features of p5.sound by showing the difference between tones generated with sine waves and triangle waves.

```
var osc, fft, waveType;
waveType = 0;

function setup() {
  createCanvas(720, 256);

  osc = new p5.TriOsc();
  osc.amp(.5);

  fft = new p5.FFT();
  osc.start();
}

function draw() {
  background(255);

  var spectrum = fft.analyze(); 
  noStroke();
  fill(0,0,255);
  for (var i = 0; i< spectrum.length; i++) {
    var x = map(i, 0, spectrum.length, 0, width);
    var h = -height + map(spectrum[i], 0, 255, height, 0);
    rect(x, height, width / spectrum.length, h )
  }

  var waveform = fft.waveform();
  noFill();
  beginShape();
  stroke(0,0,0);
  strokeWeight(1);
  for (var i = 0; i< waveform.length; i++) {
    var x = map(i, 0, waveform.length, 0, width);
    var y = map( waveform[i], -1, 1, 0, height);
    vertex(x,y);
  }
  endShape();

  var freq = map(mouseX, 0, width, 40, 880);
  osc.freq(freq);

  var amp = map(mouseY, 0, height, 1, .01);
  osc.amp(amp);
}

function mouseClicked() {
  if (waveType == 0) {
    osc.setType('sine');
    waveType = 1;
  }
  else {
    osc.setType('triangle');
    waveType = 0;
  }
}
```

1. In the setup function, create a new triangle wave oscillator named ```osc``` and set its amplitude to 0.5 (half of full volume).
2. Create a new FFT (Fast Fourier Transform) and set it to the variable ```fft```. An [FFT](https://en.wikipedia.org/wiki/Fast_Fourier_transform) is an audio analysis algorithm that lets us isolate individual audio frequencies in a sound and in this case display the sound we are hearing.
3. Start the oscillator / start making sound.
4. In the ```draw()``` function, use ```fft.analyze()``` to essentially generate an array ```spectrum``` of frequency values produced by the oscillator, then iterate through the array and draw the values in blue within the limits of our canvas. The frequency (pitch) is mapped to the x-axis while the amplitude (volume) is mapped to the y-axis.
5. Then, use ```fft.waveform()``` to generate an array of amplitude levels over brief moments in time and iterate through the array connecting each point in black. In this case, the x-axis represents time and the y-axis represents amplitude.
6. Change the frequency of the tone based on the x-position of the mouse and change the amplitude based on the y-position of the mouse.
7. Finally, the function ```mouseClicked()``` will swap the oscillating waveform between sine waves and triangle waves.
8. You'll notice that as volume increases, the waveform increases in size, and as the frequency increases, it oscillates faster and faster. More interestingly, You'll notice that sine tones only produce one frequency, its root, while triangle waves produce lots of quieter overtone frequencies dispersed at a regular interval.

For more powerful tools in writing and visualizing music, there is the external library [p5.gibber](http://charlie-roberts.com/gibber/p5-gibber/).

## p5.play

[p5.play](http://p5play.molleindustria.org) is a library that makes it possible to build 2D games through extending p5.js with a Sprite class and other features like animation support, basic collision detection and resolution, helpers for mouse and keyboard interactions, and a virtual camera. p5.play is not meant to be the most powerful game-making framework out there. From its official website: "p5.play is built for accessibility and simplicity, not performance. It is designed to be understood and possibly modified by intermediate programmers. It is not a box2D-based physics engine, it doesn't use events, nor supports 3D."

The following brief example creates sprites and positions them based on the mouse position.

```
var box1, box2;

function setup() {
  createCanvas(800,400);
  box1 = createSprite(600, 200, 50, 50);
  box2 = createSprite(200, 200, 25, 25);
}

function draw() {
  background(255,255,255);  
  box1.attractionPoint(.2, mouseX, mouseY);
  box2.attractionPoint(.4, mouseX, mouseY);
  box1.maxSpeed = 5;
  box2.maxSpeed = 6;
  
  drawSprites();
}
```

1. Name two sprites ```box1``` and ```box2```.
2. In the ```setup()``` function, create two sprites (represented as boxes with a random color) with different sizes and at different places on the canvas. If the developer has sprite image files, he/she can overlay these over each box as animations with the ```addAnimation()``` function.
3. Within each frame of animation, use the ```attractionPoint()``` function to increase the force of the box in the direction towards the mouse pointer. Limiting the box's ```maxSpeed``` will prevent this force from constantly increasing.
4. Finally, draw the sprites!

## p5.bots

Other external libraries include p5.particle which adds particle support to p5.js, and p5.speech which provides an API to Web Speech and Speech Recognition APIs. p5.js has a vibrant community so this collection of external libraries is likely to expand over the coming years.

[Previous](https://github.com/rabin2360/Presentation3/blob/master/WebGL.md) [Next](https://github.com/rabin2360/Presentation3/blob/master/p5InComparison.md)
