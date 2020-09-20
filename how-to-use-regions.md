# Regions

Regions are a class that help you define areas of arbitrary shape and size. They are created by supplying the four corners, and the hold helpful functions for connecting to other regions, transforming, and so on. Let's talk about an example rhombus with corners at (1,1), (7,2), (3,7), and (9,9)

```
   123456789
  +---------
1 |X
2 |      X
3 |
4 |
5 |
6 |
7 |  X
8 |
9 |       X
10|
```

We'd create this region like so:

```
var region = new Region(
    name: "rhombus",
    northWest: (1,1),
    northEast: (7,2)
    southEast: (9,9),
    southWest: (3,7));
```

I recommend using the parameter names when invoking to help with readability. You can use the static methods to create Regions easily from Rectangles:

`var region = Region.FromRectangle(rectangle);`

Once you have a region of any flavor, you can rotate it an arbitrary number of degrees easily:

`region = region.Rotate(22.5);`

Regions work by keeping track of the their corners (four of them), and using those to generate a collection of Inner and Outer Points. The Outer Points are the outer boundary of the Region, and the Inner Points are all the points that the region contains. Regions also have Connections and can intelligently place new connections between two regions with overlapping points.
