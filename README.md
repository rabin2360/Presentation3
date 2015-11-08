# p5.js

### Overview

p5.js is a Javascript library that allows any webpage to act as a canvas for drawing dynamic, interactive animations. p5.js was [designed to contain the following core ideas:](http://hello.p5js.org)
* Programming for the Arts
* Made for Teaching
* Extensible with Add-Ons
* Free to Download
* Open Source

p5.js is software developed by the Processing Foundation whose mission is to make coding accessible for artists, designers, educators, and beginners. It is in active development led by [Lauren McCarthy](http://lauren-mccarthy.com) and [invites contributions of all kinds.](http://p5js.org/contribute/) 

p5.js (along with other software developed by the Processing Foundation) enables [artists to create and share generative art](https://paom.com/profiles/processing/#/profile-apps), [information scientists to develop interactive data visualizations](http://gleap.org/content/podcasts_viz), [educators and scientists to build interactive physics simulations](http://natureofcode.com), web developers to add dynamic visuals to their websites, and [game developers to build graphics and animations](http://p5play.molleindustria.org). [The Processing Foundation also writes](https://processing.org/overview/) that it is used by major developers like Google to quickly prototype new interfaces, and large companies like General Electric to visualize their internal data. p5.js is unique to other similar libraries like [D3.js](http://d3js.org) in that it focuses more broadly on [bringing together a community of developers, educators, and artists,](http://p5js.org/community/) and even provides a set of guidelines for programmers to create a safe, inclusive environment.

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
