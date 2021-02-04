# Drag and Drop when Zoom Changes
## Problem
You write a funky function that allows for an object to be dragged across the stage:
````js

myStage.myObject.addEventListener("pressmove", moveDis);

function moveDis(evt){
    evt.currentTarget.x = stageX;
    evt.currentTarget.y = stageY;
}
````

And this works all fine and dandy... and then you accidentally zoom...
Hey, the function still wor- oh god where has the object gone!
Because you've zoomed in or out the object will still handle as it should across the stage, but your mouse handles different because zoom levels...

## Solution
You need to add a new function and a couple of extra lines to resolve this and use some methods that change the x/y values of the mouse/object in the global and local space.

First, a function that handles where the mouse and object is when you mouse down on the object:

````js
myStage.myObject.addEventListener("mousedown", handleMouseDown);

function handleMouseDown(evt){
	const global = myStage.localToGlobal(evt.currentTarget.x, evt.currentTarget.y);
		evt.currentTarget.offset = {
			'y': global.y - evt.stageY,
			'x': global.x - evt.stageX
		};
}
````

And then change up your movement function to handle the change in zoom level:

````js

myStage.myObject.addEventListener("pressmove", moveDis);

function moveDis(evt){
    var local = myStage.globalToLocal(evt.stageX, evt.stageY);
    evt.currentTarget.x = local.x;
    evt.currentTarget.y = local.y;
}
````

You might solve your issue using just the change to the movement function, but the handleMouseDown function will move the object without it shifting so your mouse pointer sits on a corner.

All in all this will make moving objects work regardless of window size or zoom level.