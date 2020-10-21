# TheSadRogue.Primitives

GoRogue features great support for integrating with [SadConsole](), a console-like rendering library for C#. Because so many of the objects were duplicated in both projects, the authors decided that they'd collaborate and create a [common set of primitive objects](https://github.com/thesadrogue/TheSadRogue.Primitives ) for creating, manipulating, and keeping track of locations on the grid.

Lets start with the basics:

## Points
Usage:
```
Point here = new Point(0,0);
Point there = (1,0);
Entity.Position = here;
Entity.Position = here + 1; //move diagonally right and down (or up and right if using reversed Y axis)

if(here + (1,0) == there)
{
  //there we are
}

int velocity = 40;
Point nextLocation = here + (velocity,0);
```

If you're at all familiar with the Cartesian Plane, you'll recognize the form `(X, Y)`. The first value within the parentheses is the `Horizontal` location, and the second value is the `Vertical` location. This is true for almost all other coordinate systems as well. Check out some examples:

```
  0  1  2  3  4  5  6  7  8  9
     |     |  |        |
0----------------------X <-- (7,0)
     |     |  |
1----X <-- (1,1)
           |  |
2          |  |
           |  |
3-------------X <-- (4,3)
           |
4----------X <-- (3,4)

5       X <-- (2,5)          X <-- (9,5)

6

7

8

9             X <-- (4,9)    X <-- (9,9)
```

You'll be working with `Points` quite often in GoRogue, regardless of what other classes you choose to work with.

## AdjacenyRule
__Adjacency Rules__ (within TheSadRogue.Primitives) contain logic for handling what things are __adjacent to__ one another. This is another name for [Neighborhood](https://en.wikibooks.org/wiki/Cellular_Automata/Neighborhood#2D_neighborhood) if you're familiar with Cellular Automata.

It defines an enum, `AdjacencyRule.Types`, which contains:
* __Cardinals__ - squares immediately left, right, up, and down are adjacent
* __Diagonals__ - squares immediately up-right, up-left, down-right, and down-left are adjacent.
* __EightWay__ - all squares that are either cardinally or diagonally adjacent are eight-way adjacent

#### Examples

Legend
======
* ? = Square in question
* D = Diagonally Adjacent to the Center
* C = Cardinally Adjacent to the Center
* All cells that are either C or D are 8-way adjacent to the center.

```
+---+---+---+
| D | C | D |
+---+---+---+
| C | ? | C |
+---+---+---+
| D | C | D |
+---+---+---+
```


## Area
__Areas__ are a special implementation of `IEnumerable<Point>` that provide _very_ fast operations on those points. You can think of an area as an arbitrarily-shaped section of the map.

#### Examples

Create a new area from any `IEnumerable<Point>`:
```
IEnumerable<Point> line = GetIEnumerablePoints();

Area area = new Area(line);
```

Quickly find out if a point is within the bounday:

```
if(area.Contains(point))
{
	//code
}
```

Find the common Points between two areas:

```
Area union = Area.GetUnion(leftArea, rightArea);
```

## Color

## Direction

__Directions__ help you identify which direction (north, south, etc) is which. They contain an enum, `Direction.Types`, which contain `{ None, Up, UpLeft, Left, DownLeft, Down, DownRight, Right, UpRight}`.

Directions can be added to points. For example, `(0,0) + Direction.Right` yields point `(0,1)`.

Direction also contains a static bool, `YIncreasesUpward`, that reverses the traditional RogueLike Y-direction (of increasing downards) with one that matches a cartesian plane (y increasing upwards).

## Distance

The __Distance__ class provides a few different ways of calculating the distance between two points, and some other functions. 

You'll notice that the FOV and AStar of GoRogue require a type of distance. These are talking about one of the following:

* Manhattan - movement only allowed in the cardinal directions (no diagonals)
* Chebyshev - movement allowed in all directions with no additional cost to move in diagonals
* Euclidian - Movement allowed in all directions, with diagonal movement being treated as Sqrt(2) times distance (instead of 1)

Distance also includes the helper function `Radius(Distance)` which provides the right enum to hook into your FOV calculations.

#### Example

Once you've picked which distance you'd like to measure in, you can measure how far away something is (in terms of grids on the map) like so:

```
var distanceA = Distance.Chebyshev;
double lengthAB = distanceA.Calculate(pointA, pointB);
double lengthAC = distanceA.Calculate(pointA, pointC);

if(lengthAB > lengthAC)
{
  //do the thing!
}
```

## Gradient

## Math Helpers

The Primitives library provides a few MathHelpers to make certain calculations easier.

* __MathHelper.ToDegree__ turns a radian value into it's equivalent degree value.
* __MathHelpers.ToRadian__ turns a degree angle value into a radian equivalent
* __MathHelpers.Clamp__ reduces or increases a number to be a minimum or maximum value, if it falls outside of the range
* __MathHelpers.Lerp__ provides an easy way to get the [Linear Interpolation](https://en.wikipedia.org/wiki/Linear_interpolation ) between to points
* __MathHelpers.Wrap__ allows you to keep numbers within a specified range, and wraps them from the bottom when they reach the top, and vice versa

## Palettes

## Point Extensions

## Polar Coordinates
A __Polar Coordinate__ is a pair of doubles that contains a degree of rotation, called `Theta`, and a direction from the origin, called `Radius`. Polarcoordinates provide a simple means to perform complex rotational calculations.

#### Examples
Each iteration of this loop (potentially) adds a new cell location in a spiral:

```
for(double i = 0; i < 1000; i += 0.01)
{
	PolarCoordinate here = PerformPolarFunction(i);
	yield return here.ToCartesian(); //return the equivalent `Point` from the `PolarCoordinate`
}

//elsewhere in code...

private PolarCoordinate PerformPolarFunction(double theta)
{ 
	return new PolarCoordinate(radius: theta*3, theta: theta);
}
```

## Rectangles
Delightfully simple, rectangles contain four Corners (Points) and the sides of the rectangle. All rectangles are regular in shape, with straight horizontal and vertical sides.

#### Examples
```
Rectangle garden = new Rectangle(...)
```
You can use rectangles in (examples???)