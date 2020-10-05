# Pathfinding

GoRogue provides several classes to assist with Pathfinding:

## AStar

[A* Pathfinding]() is one of the most common algorithms to find the shortest path between two points. It is a member of the `Map` object. To use it, you would have whatever `GameObject` is finding the path invoke

```
var path = CurrentMap.AStar.ShortestPath(gameObject.Position, targetPosition);
```

This gives you a `Path` object
