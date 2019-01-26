Programming Summative: P5 Programming Task
==========================================

Sketch
------
This project is based off a sketch hosted on the OpenProcessing website:

> **Name:** Magical Tree
>
> **Author:** Bárbara Almeida
>
> **URL:** https://www.openprocessing.org/sketch/313654/

The original sketch has been used and adapted under the **Creative Commons Attribution ShareAlike (CC BY-SA 3.0) license**. https://creativecommons.org/licenses/by-sa/3.0/

This project is being distributed under the same license.

Description
-----------

* The original sketch creates a static image featuring a recursively generated tree with randomly generated branches and leaves. The tree sits on the ground and has a grey radial gradient as its background.
* As the original sketch was written in Processing, the sketch has been translated into modern ES6 JavaScript.
* The sketch is now made up of several ES6 classes (the scene, the ground, the trees, the branches, the leaves), where each class is responsible for creating and drawing its own part of the sketch.
* The code has been modified to ensure it can be used as a reusable P5 component in many scenarios.
* The main class allows for several "options" objects, which change the looks and behaviour of all the parts of the main scene (including the tree/branches, the background, the ground, and the leaves). These objects can be passed as either parameters, or they are available through getters and setters. A full explanation of all options has been included below.
* The sketch is no longer a static image. Instead, branches appear to "grow" into place at the start of the sketch, magic leaves appear to hover around the tree, and the leaves now fall at random where they then land on the ground.
* Due to the use of ES6 classes, multiple trees can now be created on the scene, not just one.
* Helpful extra methods and getters/setters are now provided to allow developer using this component to manipulate it, including with their own graphics object.
* Code has been refactored and partially rewritten to be more readable and flexible (e.g. the generation of branches), and documentation has been included.
* The included example includes form controls that represent the possible options that could be passed to the sketch by a developer.

File structure
--------------

* The new JavaScript sketch has been included in `magictree.js`.
* An example has been included in `index.html` and `index.js`.
* A valid eslint configuration file (which uses the `eslint:recommended` ruleset) is present in `.eslintrc.json`, and can be checked with `npm install && npm run lint`.

Usage
-----

You can get started by creating a new instance of the Scene class. The component will automatically setup and draw itself onto the page.

```js
const scene = new MagicTreeComponent();
```

If you wish to pass your own instance of P5, you can do so here.

```js
new p5(p => new MagicTreeComponent(p));
```

You can also pass an "options" object to the constructor. These parameters determine how the component behaves and how it looks. A full explanation of all possible options has been provided below.

For convenience, you may call the `createScene` instead.

```js
new p5(p => new MagicTreeComponent(p, { /* your options here */ }));

// is equivalent to

new p5(createScene({ /* your options here */ }));
```

If you wish to integrate this component into a sketch that already has functions such as `setup()` and `draw()`, you may choose to call the draw method yourself if you wish.

```js
let scene;

function setup() {
	scene = new MagicTreeComponent(null, { scene: { bindEvents: false } });
}

function draw() {
	scene.draw();
}
```

You may also pass your own graphics object to the `draw()` method.

```js
let scene;
let graphics;

function setup() {
	scene = new MagicTreeComponent(null, { scene: { bindEvents: false } });
	graphics = createGraphics(900, 600);
}

function draw() {
	scene.draw(graphics);
	image(graphics, 0, 0);
}
```

The component exposes methods and properties that allow you to manipulate the sketch after creation. Each is explained in detail in the reference below, but as an example, this code snippet will automatically create two trees after three seconds.

```js
const scene = new MagicTreeComponent();
setTimeout(() => {
	scene.createTree(200);
	scene.createTree(700);
}, 3000);
```

Options
-------

The full options object, which can be passed to the component's constructor as a parameter, takes the structure of this object.

```js
{
	// Scene options ("sceneOptions")
	"scene": {
		"canvasWidth": 900,
		"canvasHeight": 600,
		"bindEvents": true,
		"rootPosition": 450,
		"windStrength": 2,
	},

	// Background options ("backgroundOptions")
	"background": {
		"backgroundHue": 128,
		"backgroundSaturation": 0,
		"groundHeight": 30,
		"groundColor": 20,
	},

	// Tree options ("treeOptions")
	"tree": {
		"showLeaves": true,
		"showGlow": true,
		"branchStartSize": 70,
		"branchEndSize": 0.6,
		"branchLength": 150,
		"branchChance": 0.9,
		"branchGrowthRate": 5,
		"leafMinHue": 0,
		"leafMaxHue": 255,
		"leafDiameter": 20,
		"leafGlowSize": 250,
		"leafGravity": 1,
		"leafFallChance": 0.001,
	},

	// Interaction options ("interactionOptions")
	"interaction": {
		"windEnabled": true,
		"growTreeEnabled": true
	}
}
```

You do not have to pass a full options object. If any options are omitted, the default values above are used.

```js
const scene = new MagicTreeComponent(null, { background: { backgroundSaturation: 128 } });
```

If you call the `setOptions(options)` method with a new options object after the sketch has been created, the sketch will be redrawn with the new options.

```js
const scene = new MagicTreeComponent();
scene.setOptions({ background: { backgroundSaturation: 128 } });
```

As with the object above, the options are divided into categories. If you manipulate the `sceneOptions`, `backgroundOptions`, `treeOptions` or `interactionOptions` properties of the component after the sketch has been created, the appropriate parts of the sketch may be redrawn to match the new options (i.e. if you change the `backgroundOptions` property directly, just the background will be redrawn).

```js
const scene = new MagicTreeComponent();
scene.backgroundOptions.backgroundSaturation = 128;
```

### Scene options

* `canvasWidth`: The width of the scene's whole canvas, in pixels.
* `canvasHeight`: The height of the scene's whole canvas, in pixels.
* `bindEvents`: Whether P5 hooks, such as "setup" and "draw", should be automatically bound upon creation, as a boolean.
* `rootPosition`: The x coordinate of the root of the tree that should be spawned (i.e. this determines the whole tree's overall horizontal position), as a number. This defaults to half of the `canvasWidth`.
* `windStrength`: The strength of the wind affecting leaves, where a positive number represents wind towards the right and a negative number represents wind towards the left. If the wind is following the mouse cursor, this value influences how strong the wind is, and so if a negative value is provided, the wind will go in the opposite direction to the mouse.

### Background options

* `groundHeight`: The maximum height of the ground, in pixels.
* `groundColor`: The colour of the ground. This may be a number (greyscale value), or may be a string with a named, RGB, RGBA or hex colour.
* `backgroundHue`: The hue of the background centre's colour, between 0 and 255.
* `backgroundSaturation`: The saturation of the background centre's colour, between 0 and 255.

### Tree options

* `showLeaves`: Whether leaves should be shown or not, as a boolean.
* `showGlow`: Whether leaves should have a glow, as a boolean.
* `branchStartSize`: The maximum diameter of the branch, as a number.
* `branchEndSize`: The diameter at which the branch must end, as a number.
* `branchLength`: The maximum length of a branch before either the branch ends or a new branch is created, as a number.
* `branchChance`: The chance of a branch forming another branch at the end, as a number between 0 and 1.
* `branchGrowthRate`: The rate at which branches initially grow, as a number.
* `leafMinHue` and `leafMaxHue`: The hue of leaves will be selected between the values of `leafMinHue` and `leafMaxHue`, which are both between 0 and 255.
* `leafDiameter`: The maximum diameter of the leaf, as a number.
* `leafGlowSize`: The size of the glowing effect attached to leaves, as a number.
* `leafGravity`: The number of pixels that a falling leaf moves every frame, as a number.
* `leafFallChance`: The chance of a leaf getting blown off the tree every frame, as a number between 0 and 1.

### Interaction options

* `windEnabled`: Whether the strength of the wind should depend on the position of the mouse cursor, as a boolean.
* `growTreeEnabled`: Whether clicking on the canvas should result in a new tree being grown, as a boolean.

API
---

### MagicTreeComponent

The MagicTreeComponent class is the main class of this P5 component. It is
responsible for setting up and drawing the overall scene, based on the
options provided. It encompasses all parts of the tree, the background, and
the ground.

Those implementing this P5 component may either use "createScene" above, or
they may choose to create a new instance of this class directly if they wish
to directly manipulate the scene after its creation.

#### constructor

The MagicTreeComponent class requires an instance of P5 and, optionally,
any options that should be set when drawing the scene.

Upon instantiation, the class will automatically hook into P5's events
(including setup, draw, etc.), but those instantiating this class
directly could choose to manually call the methods setup(), draw(), etc.
on the instance if they desire.

Note that this class expects that P5 is being used in instance mode
(which is why it accepts a P5 instance as a parameter). More information
about this can be found at:
https://github.com/processing/p5.js/wiki/Global-and-instance-mode

The decision to use a P5 instance was made because:
1) It may be easier to use this as a reusable P5 component. If, for
   example, the programmer implementing this component is trying to
   use this component on a complex page that already uses other sketches
   or libraries, this method ensures our component remains separate and
   could result in fewer bugs.
2) Referring to the instance "p" rather than using globally defined
   functions and constants improves readability and ensures these
   calls do not conflict with others on the page.

For an explanation on the possible options that can be passed to the
scene, please see the setOptions() method.

If a P5 instance is not provided, a new instance will be created.

##### Parameters

* **p** (Object): The instance of P5 (defaults to new instance).
* **options** (Object): An object with any additional options.

#### bindInstance

Sets the P5 instance that the component should use. This should be
generated through P5's instance mode (see examples).

Unless explicitly disabled, the instance will automatically have hooks
such as "setup" and "draw" applied. If this is undesirable, the consumer
should consider disabling the "bindEvents" option. If it's disabled, the
instance will be set up, but it is up to the consumer to manually call
methods like draw() when needed.

##### Parameters

* **p** (Object): The P5 instance to use.

#### getOptions

Returns the current full options object. Even if all options have not
manually defined, this will return a complete options object (including
any defaults).

The options object is grouped into "scene", "background", "tree" and
"interaction". See the "Options" section above for a full
explanation as to what each option within does.

##### Return value

The current, complete options object.

#### setOptions

Sets an object of options. These options will define how the sketch's
drawings should look or behave. If the object provided does not include
a particular option, a default value will be used for that option.

If the sketch already has a drawing, it will be redrawn with the new
options.

Options are categorised; see the "Options" section above for full
documentation on what each option does.

##### Parameters

* **options** (Object): An incomplete options object.

#### setup

This function is called during P5's setup phase. It will create the
overall canvas, and then start creating the images/graphics required
before drawing (such as the background, the ground, and the tree trunk).

##### Parameters

* **p5** (Object): Overrides the P5 instance used with this one.

#### draw

This function is called during P5's draw phase. It will, in turn, call
the draw function on every tree on the scene. It will also render
constant static parts of the scene, like the background.

##### Parameters

* **p5** (Object): Overrides the P5 instance used with this one.

#### mousePressed

This method is called when P5 detects a mouse press. It will create a
tree at the cursor's current position, if enabled and if the click took
place within the canvas.

#### mouseMoved

This method is called when P5 detects that the mouse has moved. It will
change the wind strength to follow the cursor, if enabled. Since the
wind strength can be negative, this will also change the direction.

#### create

This function is responsible for initializing the constant parts of the
scene, outside of the tree. This includes the background and the ground.

Note: The component calls this method internally; consumers might not need
to use it.

#### createBackground

Creates the background image. This works by creating a static image
consisting of several coloured ellipses from the centre, where the
ellipses gradually become slightly darker. This creates a subtle overall
"inner shadow" effect.

Note: The component calls this method internally; consumers might not need
to use it.

#### getTrees

Returns an array containing all the trees that are currently present on
the scene.

##### Return value

An array of instances of the Tree class.

#### getGround

Returns the instance of the ground currently drawn.

##### Return value

An instance of the Ground class.

#### getBranches

A single Tree may consist of three individual "sub-trees". On the
sketch, these trees are slightly different colours and have different
branch layouts. This method gets the array of Branch instances that are
associated with a given sub-tree.

##### Parameters

* **subTree** (number): The index of the tree to return branches for.

##### Return value

An array of Branch instances.

#### createTree

Creates a new tree. This uses the scene's current options to create a
new instance of the tree class. After calling this function, this tree
will be drawn onto the scene from now on.

This is automatically called when the scene is created, but may also be
called again after that.

If a root position is not explicitly provided, the initial root position
defined within the options object will be used.

##### Parameters

* **rootPosition** (number): The x coordinate of the tree's root.

#### clearAdditionalTrees

Clears any trees that have been created in addition to the initial tree.
This works by deleting all trees that have been created and then
recreating an initial tree in the centre.

### Tree

The Tree class represents a single tree, and contains the methods required
to draw it. Every tree is also responsible for generating all the leaves it
has.

#### constructor

The Tree class is usually instantiated by the MagicTreeComponent class.
It is instantiated with the P5 instance to draw the tree onto, and the
options (which follows the same format as the scene's options).

If a root position is not explicitly provided, the initial root position
defined within the options object will be used.

##### Parameters

* **p** (Object): The P5 instance that the tree should be drawn onto.
* **options** (Object): The options object.
* **rootPosition** (number): The position of the tree's root.

#### create

Calling this function will perform the setup required to create a new
tree. This includes selecting the minimum and maximum hue of the tree's
leaves, and ensuring no leaves already exist. Then, the tree will be
created.

Note: The component calls this method internally; consumers might not need
to use it.

#### draw

Draws the tree and its features onto the canvas. This method will be
called repeatedly (within P5's draw hook).

Note: The component calls this method internally; consumers might not need
to use it.

##### Parameters

* **ground** (Object): An instance of the Ground that leaves fall on.
* **p5** (Object): Overrides the P5 instance used with this one.

#### drawTree

Draws an array of branch objects onto the tree, if they have not
already been drawn yet.

This method expects that branch objects provided were already generated
during the tree's setup.

If the tree is "growing", branches are repeatedly drawn until they reach
their full size.

Note: The component calls this method internally; consumers might not need
to use it.

##### Parameters

* **branches** (Object[]): An array of all branches on this tree.
* **color** (number): The colour of the tree.
* **subTree** (number): The index of the sub tree to draw onto.

#### setHue

Uses the minimum and maximum leaf hue defined in the options (or the
defaults if none have been explicitly set) to randomly select the
minimum and maximum hue of this tree's leaves. In other words, a random
range of possible hues will be selected for this tree, and all leaves
will have a hue between this range (but will not all be the same).

#### getWindStrength

Gets the current additional wind strength influencing this tree.

##### Return value

The current wind strength.

#### setWindStrength

Sets the current wind strength. This will be used in combination with
the wind strength set in the options object. If the wind strength is
negative, leaves blow to the left.

##### Parameters

* **windStrength** (number): The current wind strength.

#### createTree

Creates a new tree (replacing any tree that has already been drawn),
using the options provided. This works by effectively drawing three
trees in the same position, where the trees underneath have a lighter
fill colour (creating the illusion of depth in the tree).

Note: The component calls this method internally; consumers might not need
to use it.

#### drawLeaves

Draws all the leaves onto the tree. This works by iterating through all
the leaves that have been created previously (since leaves are created
while branches are generated). For each leaf, it will determine the hue
of the leaf within the predetermined range (since each leaf has a
slightly different hue), perform any gravity checks, and call the draw
method.

Note: The component calls this method internally; consumers might not need
to use it.

##### Parameters

* **minDiam** (number): The minimum diameter of the leaves.
* **maxDiam** (number): The maximum diameter of the leaves.
* **minAlpha** (number): The minimum alpha (opacity) of the leaves.
* **maxAlpha** (number): The maximum alpha (opacity) of the leaves.
* **ground** (string): The Ground instance, for calculating falls.
* **p5** (Object): Overrides the P5 instance used with this one.

### Branch

An instance of the Branch class represents a single branch as part of a
tree. It is responsible for generating and drawing the branch. Additionally,
an instance may contain several child branches (i.e. a Branch instance may
contain other Branch instances).

#### constructor

Every branch consists of "segments", where each segment is a circle that
will be drawn as part of the branch. Segments each have an x coordinate,
a y coordinate, and a diameter. Upon instantiation, a branch has no
segments (so this is initialised as an empty array).

Additionally, a branch could have child branches, and so an array (which
may eventually contain further Branch instances) is also initialised.

How far the branch has grown so far ("growth") is initialised at zero,
as this represents the index of the next segment to be drawn.

##### Parameters

* **p** (Object): The P5 instance that the branch should be drawn onto.
* **options** (Object): The scene's options object.
* **n** (number): The seed used to randomly generate the branch.

#### getChildBranches

Returns all the child branches attached to this branch.

##### Return value

- An array of Branch instances.

#### getIsDrawn

Returns whether all segments in the branch have been drawn at least
once yet.

##### Return value

- Whether the branch has been drawn.

#### getIsGrown

Returns whether all segments in the branch have been fully drawn and
grown to the maximum diameter.

##### Return value

Whether the branch has grown.

#### getLeaf

Returns the Leaf instance of the leaf attached to this branch, if any.

##### Return value

The leaf instance.

#### create

Recursively creates new branches and leaves.

Branches consist of a series of closely packed ellipses. This works
because the method recursively calls itself with a slightly different
position (i.e. the coordinates of the next ellipse to draw), until the
current branch reaches its maximum length.

Once the maximum length has been reached, the branch might randomly spawn
a left branch and might also randomly spawn a right branch. The process
restarts for each extra branch (if any). Extra branches have a thinner
diameter, a smaller maximum length, and are at a different angle. If no
additional branches are spawned, the method draws the tip of the branch.

Once the branch is sufficiently thin, the branch ends and places a leaf.

Note: The component calls this method internally; consumers might not need
to use it.

##### Parameters

* **x** (number): The x coordinate of the start of the branch.
* **y** (number): The y coordinate of the start of the branch.
* **branchSize** (number): The approximate diameter of the branch.
* **theta** (number): The angle of the direction of the branch.
* **branchLength** (number): The maximum length of this branch.
* **pos** (number): The progress of this branch so far (initially 0).

##### Return value

Returns an object representing this branch.

#### createChild

This method will start the creation of a child branch, if the random
threshold specified in the scene options is met.

This works by initialising a new instance of the Branch class and
creating the branch, which means that this will effectively recursively
create new branches (until either the base case of "create" is reached
or we randomly determine that a branch has no children).

The "direction" provided determines in which direction the child branch
should head towards relative to the current branch's angle.

Note: The component calls this method internally; consumers might not need
to use it.

##### Parameters

* **x** (number): The final x coordinate of the existing branch.
* **y** (number): The final y coordinate of the existing branch.
* **branchSize** (number): The final size of the existing branch.
* **theta** (number): The angle of the existing branch.
* **branchLength** (number): The maximum length of the existing branch.
* **direction** (number): Constant to help determine the new angle.

#### drawBranch

Draws this branch onto the tree.

Branches consist of "segments", where each segment represents an
individual ellipse (part of the branch) that needs to be drawn. Segments
are drawn in order, so they gradually appear one by one.

The "growth" of a segment determines the current diameter of the
ellipse. Therefore, the "growth" increases until it reaches the maximum
diameter in the branch object.

Note: The component calls this method internally; consumers might not need
to use it.

##### Parameters

* **tree** (Object): The graphics object to draw the branch on.

##### Return value

Whether the end of the branch has been reached.

#### drawBranchTip

Adds a tip to the end of the branch. The tip is constructed by drawing a
quadrilateral and rotating it to match the branch. The tip is drawn at
the last segment of the branch (so the tip is always at the end of the
branch).

Note: The component calls this method internally; consumers might not need
to use it.

##### Parameters

* **tree** (Object): The graphics object to draw the branch on.

### Leaf

The Leaf class represents a single leaf floating on a tree. Trees
instantiate leaves while the tree is being generated, and so this should not
be instantiated directly from outside the component.

#### constructor

Leaves accept a P5 instance upon which the leaf will be drawn, and a
vector which contains the initial position of the leaf.

##### Parameters

* **p** (Object): The P5 instance that the tree should be drawn onto.
* **vector** (Object): The initial vector position of the leaf.

#### draw

The draw method will be called repeatedly (within P5's draw method).
It will draw the current state of the leaf onto the P5 canvas.

The minimum and maximum diameter and alpha values provided will be used
to randomly determine how the leaf appears, based on the leaf's noise.

Note: The component calls this method internally; consumers might not need
to use it.

##### Parameters

* **minDiam** (number): The minimum diameter of the circle.
* **maxDiam** (number): The maximum diameter of the circle.
* **minAlpha** (number): The minimum alpha (opacity) of the leaf.
* **maxAlpha** (number): The maximum alpha (opacity) of the leaf.
* **hue** (number): The hue of the leaf.
* **p5** (Object): Overrides the P5 instance used with this one.

#### fall

This method should be called to perform any calculations relating to
gravity or movement of the leaf. It may cause the leaf to randomly fall,
and if this leaf is falling, the leaf will slowly move until it collides
with the ground.

Note: The component calls this method internally; consumers might not need
to use it.

##### Parameters

* **ground** (Object): An instance of the ground.
* **wind** (number): The current horizontal wind speed.
* **fallSpeed** (number): The speed at which the leaf is falling.
* **fallChance** (number): The chance of the leaf falling in this tick.

### Ground

The Ground class represents the static ground that appears below all trees,
at the bottom of the scene. It is randomly generated, and this is created
once by the scene.

#### constructor

The ground has both a maximum height (since the height of the ground
appears to vary), and the colour of the ground. The constructor also
initialises a variable for the noise of the ground's height.

##### Parameters

* **height** (number): The maximum height of the ground.
* **color** (string): The colour of the ground.

#### draw

Generates the ground and draws it onto the P5 instance provided. As the
ground is static, repeatedly calling this afterwards is unnecessary.

This works by dividing the ground up into segments, and drawing a vertex
for each segment, where the y coordinate of each vertex varies slightly.
This creates the illusion of a rough ground.

The y coordinates of each vertex is stored so that it can be used for
collision checking elsewhere.

Note: The component calls this method internally; consumers might not need
to use it.

##### Parameters

* **p** (Object): The instance of P5 to draw the ground onto.

#### isColliding

Returns whether the ground that was last drawn intersects with the x and
y coordinate given.

##### Parameters

* **x** (number): The x coordinate to check.
* **y** (number): The y coordinate to check.

##### Return value

Whether or not the coordinates are colliding.
