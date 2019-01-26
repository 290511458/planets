# Typo.js

## Introduction
Typo.js is an openprocessing sketch altered to be as reusable as possible, it uses javascript classes and is heavily parameterised to allow it to be easily added to another sketch without much difficulty.

It is a tool which allows the user to draw, but with text which can be entered as a parameter when the object is initialised.

## usage

- To use typo.js first p5 must be imported:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/0.7.2/p5.js"></script>
```

- Then typo.js must be imported:

```html
<script src="typo.js"></script>
```
*assuming typo.js is in the same directory*

- Then inside p5.js' setup function, a canvas must be created and a new typo object must be initialised with the correct values for the parameters
```javascript
function setup() {
    createCanvas(640,480)
    t = new typo("Example text...",   2,               0)
    ///          text,                min font size,   distortion angle
```

- The objects draw function must be called inside the function called by p5 e.g. ```draw()```
```javascript
function draw() {
    t.draw()
} 
```

- Events must be passed through to the object
```javascript
function keyPressed() {
    t.keyPressed()
}
function mousePressed() {
    t.mousePressed()
}
function keyTyped() {
    t.keyTyped()
}
```
 ### Parameters
The possible parameters are:
- **text**  
    - the text to be printed (this is repeated so the length is unimportant)
    - default value of 
        *"Mon propos dans les pages qui suivent a plutôt été de décrire le reste : ce que l'on ne note généralement pas, ce qui ne se remarque pas, ce qui n'a pas d'importance : ce qui se passe quand il ne se passe rien, sinon du temps, des gens, des voitures et des nuages."*
- **min font size** 
    - the smallest size the font will reach
    - default value of 3
- **Distortion angle** 
    - the maximum angle the letters can reach away from the direction of movement of the mouse curser (randomised between 0 and this parameter).
    - default value of 0

### Getters and Setters

all three of these values can be got or set via getter and setter functions, these are:
```javascript
getText()
setText("NewText")

getMinFontSize()
setMinFontSize(15)

getDistortionAngle()
setDistortionAngle(1)
```

### Other functions

The other functions must all be called in the p5 functions of the same name.
```javascript
function draw() {
    t.draw()
} 
function keyPressed() {
    t.keyPressed()
}
function mousePressed() {
    t.mousePressed()
}
function keyTyped() {
    t.keyTyped()
}
```
