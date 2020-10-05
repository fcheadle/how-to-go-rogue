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

## Color

## Direction

## Distance

## Gradient

## Math Helpers

## Palettes

## Point Extensions

## Polar Coordinates

## Rectangles
Delightfully simple, rectangles contain four Corners (Points) and the sides of the rectangle. All rectangles are regular in shape, with straight horizontal and vertical sides.

Usage:
```
Rectangle garden = new Rectangle(...)

```
