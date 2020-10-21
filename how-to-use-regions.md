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
    northEast: (7,2),
    southEast: (9,9),
    southWest: (3,7));

//functionally identical to
var region = new Region("rhombus",(1,1),(7,2),(9,9),(3,7));
```

I recommend using the parameter names when invoking to help with readability.

Regions work by keeping track of the their corners (four of them), and using those to generate collections of Inner and Outer Points. The Outer Points are the outer boundary of the Region, and the Inner Points are all the points that the region contains. Regions also have a collection of Points called `Connections` which can be used in terrain generation algorithms to make a path between two rooms.

You can use the static methods to create Regions easily from Rectangles:

`var region = Region.FromRectangle(rectangle);`

Once you have a region of any flavor, you can rotate it an arbitrary number of degrees easily:

`region = region.Rotate(22.5);`

Regions keep a collection of `SubRegions`. Any transformation performed on the parent region also transforms all subregions. You would use this in cases where you _inherit from_ Region and have functionality in this new class to generate more detailed regions.

```
class House : Region
{
    public House(Point northWest, Point northEast, Point SouthWest, Point southEast) : base(northWest, northEast, southEast, southWest)
    {
    	GenerateRooms(); //adds subregions to regions
    }
}

//elsewhere in the code...

var house = new House((0,0), (40,0), (40,40), (0,40)).Rotate(30, (80,80));
//ever room in the house also rotates with the house
```

