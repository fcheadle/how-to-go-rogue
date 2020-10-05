# How to use AdjacencyRule
__Adjacency Rules__ (within TheSadRogue.Primitives) contain logic for handling what things are __adjacent to__ one another. This is another name for [Neighborhood](https://en.wikibooks.org/wiki/Cellular_Automata/Neighborhood#2D_neighborhood) if you're familiar with Cellular Automata.

It defines an enum, `AdjacencyRule.Types`, which contains:
* __Cardinals__ - squares immediately left, right, up, and down are adjacent
* __Diagonals__ - squares immediately up-right, up-left, down-right, and down-left are adjacent.
* __EightWay__ - all squares that are either cardinally or diagonally adjacent are eight-way adjacent


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

