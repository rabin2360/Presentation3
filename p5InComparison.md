# p5.js Compared to Similar Frameworks

## Processing

Processing is an open source programming language built on Java that has been in development since 2001. Processing has a huge community, a large body of example work and tutorials, and a powerful IDE. P5.js is arguably a more powerful next step to Processing since it expands the canvas of Processsing from a desktop app to anywhere in the browser. However, many objects in Processing are not yet supported in p5.js, so translating programs from Processing to p5.js is not always easy or even possible. (An attempt by us to translate the [Wikipedia Map example](https://en.wikipedia.org/wiki/Processing_(programming_language)) to p5.js ended up a disaster since p5.js does not yet support the ability to work with SVG files.) Since the Processing Foundation understands that many new p5.js users have already used Processing, they have [uploaded a useful transition guide.](https://github.com/processing/p5.js/wiki/Processing-transition)

The following is an example of making fractals from [Daniel Shiffman's excellent book The Nature of Code](http://natureofcode.com/book/chapter-8-fractals/) translated to p5.js.

```
// replace void setup() with function setup()
function setup() {
  // replace size() with createCanvas
  createCanvas(800,800); 
}
 
function draw() {
  background(255);
  drawCircle(width/2,height/2,200);
}
 
function drawCircle(x, y, radius) {
  // All of this code is identical
  stroke(0);
  noFill();
  ellipse(x, y, radius, radius);
  if (radius > 8) {
    drawCircle(x + radius/2, y, radius/2);
    drawCircle(x - radius/2, y, radius/2);
    drawCircle(x, y + radius/2, radius/2);
    drawCircle(x, y - radius/2, radius/2);
  }
}
```

![Fractal Image](https://github.com/rabin2360/Presentation3/blob/master/Presentation3/ProcessingExample.png)

## Processing.js

[Processing.js]((http://processingjs.org) ) is a port of the Processing Language, [and a quick look at its GitHub page](https://github.com/processing-js/processing-js/) reveals that its most recent version was released in March 2015. Unlike p5.js, Processing.js is not developed by the Processing Foundation. Also unlike p5.js which is meant to be a full version of Processing in Javascript, it is actually a converter that interprets Processing code into JavaScript. So, if you already know Processing, you already know Processing.js.

#### Advantages over p5.js

* Processing.js supports many more objects and functions from the original Processing language than p5.js. (But this will likely change over the next couple years as p5.js continues its development.)
* If you have already written programs in Processing, porting them to your website is much easier with Processing.js.
* Some testing has shown that [Processing.js performs slightly better.](http://www.sitepoint.com/processing-js-vs-p5-js-whats-difference/)

#### Disadvantages

* Unlike p5.js, Processing.js is not capable of HTML DOM manipulation. [Websites such as this would not be possible.](http://p5play.molleindustria.org)
* Processing.js is not supported by the Processing Foundation and so its future development is up in the air.

In general, we think that p5.js is a better choice and will continue to get better.

## D3.js

[D3.js](http://d3js.org) (Data-Driven Documents) is a Javascript Library for producing dynamic, interactive data visualizations. D3.js is minimal focusing on the challenge of manipulating documents based on data and making it as simple as possible to bind data to the DOM and transform it on the fly. D3.js contains the following principles:
* Selections: Similar to jQuery, the programmer can quickly operate on broad or specific parts of the DOM called "Nodes."
* Transformation: Unlike p5.js, D3.js does not introduce a new visual representation, but rather utilizes web standards (HTML, SVG, and CSS).
* Transitions: D3.js easily extends transformations to animated transitions of representations of data for example gradually fading in a page color or staggering the introduction of new data points in a graph.
* Data-binding: Elements from loaded datasheets are associated with SVG files that have various controllable properties and behaviors.

One major difference between D3.js and p5.js is in their philosophies: P5.js is meant to be accessible to people new to coding while most of the language on the [D3.js website](http://d3js.org) is only understandable to relatively experienced web developers. D3.js is probably the best option when creating high performing data visualizations as it is much smaller and focused than p5.js. However, p5.js consists of many more features and is more worthwhile for new programmers to learn.

## CreateJS

[CreateJS](http://www.createjs.com) is a suite of open-source libraries that contain much of the same functionality as p5.js  and utilize HTML5 to create interactive content. Libraries such as EaselJS (graphics and interactions), TweenJS (tweening) SoundJS (audio playback), and PreloadJS (preloading assets) can all be used together or mixed and matched. The API for CreateJS is very similar to Flash. CreateJS and p5.js have similar features, so it is hard to pick an immediate winner, but in the future as Flash becomes less relevent, p5.js may align more with developers' skillsets. 

[Previous](https://github.com/rabin2360/Presentation3/blob/master/p5Addons.md) [Next](https://github.com/rabin2360/Presentation3/blob/master/Conclusion.md)
