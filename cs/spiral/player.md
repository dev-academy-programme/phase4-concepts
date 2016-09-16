Now that we have a board, it's time to add the protagonist. In the running program we'll need a `player` object, so to create the object we'll need a `Player` class. The class will need a way to track the player's current position on the board: we suggest you create properties for `Row` and `Col`.

Write a test that checks to see that a newly instantiated object of class `Player` has both these properties set to 0. Remember, you'll need to create a new class file called `PlayerTests` in the `SpiralTests` project. The framework for your test will look like this:

```cs
using Spiral;
using Xunit;

namespace SpiralTests
{
    public class PlayerTests
    {
        [Fact]
        public void PlayerStartsAt0 ()
        {
            // Arrange & Act
            var player = new Player();

            // Assert
			// ...
        }
    }
}
```
Write assertions to make sure the properties on `player` are 0 after it's created. To make the test pass, presumably you'll need to write a constructor for your Player class that takes no arguments... 

When you've got the test passing, it's time to teach your player how to move. Write a new test that checks to see what `Row` and `Col` are set to after a method named `Move` is called with the argument 's' (for 'south'). Don't forget, you won't ever want the player to move to a location with a negative number! Make the test pass, then write another one each for `Move('e')`, `Move('n')`, and `Move('w')`. Then if you want even more practice (and you want your player to be able to move diagonally) write tests for `Move('nw')`, `Move('ne')`, `Move('sw')`, and `Move('se')`. Repetition is great for getting the basics down!

In the `Arrange` part of some tests, you might need to set artificial starting values for `Row` and `Col`. After all, you can hardly move 'north' if your player is already at 0,0! One way would be to define a constructor that accepts two arguments, one each for `Row` and `Col`. Another would be to simply make the properties public, if they aren't already, and set them directly:

```cs
player.Row = 5;
player.Col = 4;
```

For each step, make the test fail, make it pass, refactor anything that you think needs it, and do a Git commit. Be strict with yourself: good habits are especially important when no-one else is watching! Behave as if a potential employer will be looking at your commit history (which might very well be true).