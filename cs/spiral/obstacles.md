So far the player exists in a featureless landscape of dots. Let's change that with some objects the player must navigate around. We can use obstacles to construct walls and rooms.

Creating obstacles should be very similar to the way we created the player. The only real difference is that they don't move around, so it should be even easier! Create a new class file, `Obstacle.cs`, and a corresponding test class. You first test should just make sure that the obstacle's `Row` and `Col` properties are set correctly in the constructor. You probably shouldn't make a constructor that takes no arguments: unlike the player, we always want to specify where our obstacles are.

That simple beginning out of the way, we have to teach the board to store the obstacles. Write a test that expects `Board` to allow a constructor that passes a `List<Obstacle>` and stores the obstacles internally as an `IEnumerable<Obstacle>`: a _generic collection_. We don't much care about how many obstacles there are, only that there can be some and we can grab them all from a collection when we need them.

We'll start with a rather obvious test just to get the `Obstacles` property set up on the board:

```cs
// LINQ needed for .Count()
using System.Linq;

[Fact]
public void BoardCanHaveObstacles () 
{
	// Arrange
	var obstacles = new List<Obstacle> { new Obstacle(0, 0) };

	// Act
	var board = new Board(1, 1, obstacles);

	// Assert
	Assert.Equal(1, board.Obstacles.Count());
}
```

This is the kind of test that we don't always need to write in C# because it's fairly self-evident that if a class has a property, we can set that property. Still, it doesn't hurt to practice and it might help if you're not used to the syntax for collections yet. To make it pass, you'll need to add a constructor for `Board` that accepts integers for row, col, and a collection of obstacles.

The next step is to make sure that your player can't move into a location that contains an obstacle... otherwise they'd be pretty ineffectual obstacles. Write a test in `BoardTests` that attempts to move your player onto an obstacle, and make sure that the player's location doesn't change.