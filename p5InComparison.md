# P5 Compared to Other Similar Frameworks

### Processing

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

### Processing.js

### D3.js

### EaselJS
