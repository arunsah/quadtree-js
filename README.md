# quadtree-js

This is a JavaScript Quadtree implementation based on the Java Methods described on [gamedevelopment.tutsplus.com by Steven Lambert](https://gamedevelopment.tutsplus.com/tutorials/quick-tip-use-quadtrees-to-detect-likely-collisions-in-2d-space--gamedev-374):

> Many games require the use of collision detection algorithms to determine when two objects have collided, but these algorithms are often expensive operations and can greatly slow down a game. One way to speed things up is to reduce the number of checks that have to be made. Two objects that are at opposite ends of the screen can not possibly collide, so there is no need to check for a collision between them. This is where a quadtree comes into play.

This implementation can store and retrieve rectangles in a recursive 2D Quadtree. Every Quadtree node can hold a maximum of number objects before it splits into four subnodes. Objects are only stored on leaf nodes (the lowest level). If an object overlaps into multiple leaf nodes, a reference to the object is stored in each node. 

## Demos

* [Simple Demo](http://timohausmann.de/quadtree.js/simple.html) – add static objects and see the Quadtree split
* [Dynamic Demo](http://timohausmann.de/quadtree.js/dynamic.html) – continuously track moving objects
* [Benchmark v1.2](http://timohausmann.de/quadtree.js/test-10000-1.2.0.html) - Performance test with 10.000 objects
* [Benchmark v1.1.3](http://timohausmann.de/quadtree.js/test-10000-1.1.3.html) - Performance test with 10.000 objects (old implementation)

## Install

[Now also available on npm](https://www.npmjs.com/package/@timohausmann/quadtree-js)! Install this module via npm and import or require it:

````
npm i -D @timohausmann/quadtree-js
````

````
import Quadtree from '@timohausmann/quadtree-js';
````

````
const Quadtree = require('@timohausmann/quadtree-js');
````

Alternatively, [download the source](https://github.com/timohausmann/quadtree-js/archive/master.zip) and include it the old-fashioned way:

    <script src="quadtree.min.js"></script>

## How to use

Create a new Quadtree with default values for max_objects (10) and max_levels (4)
<pre>
var myTree = new Quadtree({
	x: 0,
	y: 0,
	width: 400,
	height: 300
}, 10, 4);
</pre>

> MAX_OBJECTS defines how many objects a node can hold before it splits and MAX_LEVELS defines the deepest level subnode.

If you want to specify `max_objects` and `max_levels` on your own, you can pass them as a 2nd and 3rd argument. Increasing `max_levels` may have an impact on performance depending on your objects. Using a low value for `max_levels` increases the Quadtree performance but will most likely return more candidates.

<pre>
var myTree = new Quadtree({
	x: 0,
	y: 0,
	width: 800,
	height: 600
}, 15, 6);
</pre> 

Insert an element in the Quadtree
<pre>
myTree.insert({
	x: 200,
	y: 150,
	width: 20,
	height: 20
});
</pre>

Retrieve elements from nodes that intersect with the given bounds
<pre>
var elements = myTree.retrieve({
	x: 150,
	y: 100,
	width: 20,
	height: 20
});
</pre>

Clear the Quadtree
<pre>
myTree.clear();
</pre>

Check out the examples for more information.

## Browser Support

This library is supported in all modern browsers beginning from IE9 and above. 

## Changelog

### 1.2.0

This implementation now stores objects exclusively on leaf nodes and thus differs from the tutorial it's based on. Objects, that overlap into multiple subnodes are now referenced in each matching subnode instead of their parent node. This drastically reduces the collision candidates. Prior to 1.2.0, overlapping objects were stored in parent nodes. 

### 1.1.3

Support for npm and `module.exports`

## Update single objects

There is a (currently deprecated) [quadtree-js hitman branch](https://github.com/timohausmann/quadtree-js/tree/hitman) available that allows you to update and remove single objects. This may be handy when most of the objects in your Quadtree are static. Please raise an issue if you want to see this feature maintained in future releases.