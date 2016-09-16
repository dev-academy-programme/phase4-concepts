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

When you've got the test passing, it's time to teach your player how to move. Write a new test that checks to see what `Row` and `Col` are set to after a method named `Move` is called with the argument 'n' (for 'north'). Don't forget, you won't ever want the player to move to a location with a negative number! Make the test pass, then write another one each for `Move('s')`, `Move('e')`, and `Move('w')`. Then if you want even more practice (and you want your player to be able to move diagonally) write tests for `Move('nw')`, `Move('ne')`, `Move('sw')`, and `Move('se')`. Repetition is great for getting the basics down!