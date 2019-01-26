**Snake Game**
==============

## How To Play
* Use up down left right to control the green snake

## Aim
* To collect the yellow point

## Description

The developed game is the implementation of the popular Snake game in which the
player has to control the snake on the screen in order to survive in the game.
Once the snake hits any one of the borders of the game area the game starts
again. The length of the snake will increase every time it eats a food item that
appears in the game area.

## Implementation and Controls 

In order to design the game area on HTML page, the canvas element is utilized.
The Canvas element is to very useful in drawing graphics on the simple web pages
through the use of the java scripts. This element is used as a container for the
graphics which needs to represented on the simple html page. For this project,
the used scripts are snake.js, index.js in order to draw the graphics of
the snake game. In order to develop the game faster several available methods
are used in order to draw the paths, boxes for the body of the snake and adding
images.

In the next stage the of the development the main concern was determining
players intended movement for the snake which will be reflected on the game area
or canvas and this was the most challenging part of the project.

For the first section of this part, the code and algorithm is developed in order
to determine direction in which the user wants to change. This stage is
completed through the comparing the values from the user input from the key
stroke to find the high or low or any other directions of the snake.

In case the HTML page is not available on the browsers, then the user must
ensure that the path of all the JavaScript and css files are correct as well as
they are in the same folder. The game cannot be played on the Internet explorer,
the bundled browser with the windows operating system. As it is one of the
non-standards compliant browser that lacks support for
DOMObject.addEventListener() using which the user input for the game is
evaluated. Other browsers like opera, safari, chrome and Mozilla Firefox can be
used to play the game.

In case of a key stroke is received to change the direction, then the input is
evaluated in the logic implemented in the program developed using the JavaScript
to find out if the user input is valid change in the direction depending on the
snakes current positions and if the direction change is possible from that
location of canvas. For example, if the user cannot move downwards if the snake
is going up therefore depending on the user input the snake would not change
directions.

After the detection of the any collision the game cycle again generated a new
cycle with the condition that the game has not finished with the three terms.
Using the following code section, the collision detection is achieved in order
to manage the movement and drawing of the snake.
