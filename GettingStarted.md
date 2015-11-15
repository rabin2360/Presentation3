### Getting Started

1. Download [p5.js Complete](http://p5js.org/download/), a directory containing p5.js, p5.dom.js, p5.sound.js, and an example project.
2. Navigate to the empty example directory and open up index.html and sketch.js in your favorite editor.
3. In sketch.js uncomment the lines ```createCanvas(windowWidth, windowHeight);``` and ```ellipse(width/2, height/2, 50, 50);```
4. Within index.html, you may want to change the p5.js file your application links to to the minified file which is compressed for faster page loading or the CDN hosted file.
  * ```<script src="../p5.min.js"></script>```
  * ```<script src="http://cdnjs.cloudflare.com/ajax/libs/p5.js/0.4.17/p5.js"></script>```
5. Serve the the entire p5-release directory.
  * We tend to like using Python: ```$ python -m SimpleHTTPServer```
6. Navigate to ```http://127.0.0.1:8000/empty-example/index.html``` (or whatever port is being served) in a web browser where you should simply see a circle displayed in the center of the screen.
  * Alternatively, with a program this simple, you can just open index.html with any web browser.

[Previous](https://github.com/rabin2360/Presentation3/blob/master/README.md)  [Next](https://github.com/rabin2360/Presentation3/blob/master/Overview.md)
