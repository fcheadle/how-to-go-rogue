# How to use Area
__Areas__ (defined in TheSadRogue.Primitives) are a special implementation of `IEnumerable<Point>` that provide very fast operations on those points. You can think of an area as an arbitrarily-shaped section of the map.

You use an Area when you need to perform _fast_ operations on sets of `Point`s. 