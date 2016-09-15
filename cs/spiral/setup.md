### Setup

To begin with, create a new solution. You can call it what you like: in keeping with the Enspiral theme, we'll call ours `Spiral`. You may as well follow the uppercase convention for .NET solution/project names, most everyone else does.

 - For the project type, remember to choose _Console Application_.

In the solution explorer, right-click the solution name and choose _Add_, then _New Project_. Choose _Class Library_ for the project type, and name it `SpiralTests`.

Right click `SpiralTests` in the solution explorer. Choose _Add_, then _Reference_. You should see a popup with a checkbox labelled `Spiral` (if you don't, click _Projects_ / _Solution_ on the side). Check the box, then click _OK_. This lets `SpiralTests` _reference_ namespaces, classes and methods in the `Spiral` project.

We need to add the [xUnit](https://xunit.github.io/) package to do our testing with. Right click on the `SpiralTests` project and choose _Manage NuGet packages_. Click _Browse_ on the left side, then type 'xunit' in the search box. Select the xUnit package and click _Install_. While you're at it, do the same thing for _xunit.runner.visualstudio_.

So, let's write our first test! In `SpiralTests`, rename `Class1.cs` to `ProgramTests`. If it offers to rename other things for you, choose _Yes_. Make `ProgramTests` look like this:

```cs
using Xunit;

namespace SpiralTests
{
    public class ProgramTests
    {
        [Fact]
        public void Working ()
        {
			Assert.True(true);
        }
    }
}
```

Go to the test explorer and choose _Run All_. The test you've just written will be discovered and run after the project builds. Hopefully you should see a little green tick.

So there's a bit going on here. Tests are normally given the _decorator_ `[Fact]`. They have accessibility `public` and don't return anything. If you're familiar with tape testing in JavaScript, the above test is equivalent to:

```js
test('Working', t => {
  t.ok(true)
})
```

Let's write one that does something a bit more useful. In C#, many of the tests we might write in JavaScript are not quite as useful because the static typing takes care of quite a bit of checking for us at compile time. For example, we don't need to check that a method returns a string: we _know_ it does, because it has return type string:

```cs
public string GetDescription ()
{
	return "I'm a description."
}
```

Still, there are plenty of things to test. How about this?

```cs
        [Fact]
        public void BoardGeneratedWithCorrectDimensions ()
        {
            // Arrange & Act
            var board = new Board(5, 5);

            // Assert
            Assert.Equal(5, board.Cells.Length);
            Assert.Equal(5, board.Cells[0].Length);
        }
```

This will cause lots of red lines to show up underneath some of the names! This is because Visual Studio can tell ahead of time many of the compile errors that will be caused, and tries to warn you about them. Remember _RED_, _GREEN_, _REFACTOR_? You can think of this as the 'RED' part! We are effectively making the test fail first, because the class we're trying to test doesn't exist yet. You can certainly run the test anyway, but the build will fail with a couple of errors.

To make the test pass, do the _minimum amount_ necessary to get the test to pass. This will mean:
 - creating a new _class_,  `Board`, in the `Spiral` project
 - creating a new _property_, `Cells`, in the `Board` class. The property should be a [_jagged array_](https://www.dotnetperls.com/jagged-array)
 - creating a _constructor_ for the `Board` class that accepts two integers as parameters
 - returning a jagged array with five rows, the first of which (at least) has five columns

After you get that passing, you'll obviously need to handle different dimensions at some point so write another test that forces you to code a more complete constructor, if you haven't already:

```
        [Fact]
        public void BoardGeneratedSixByTwo ()
        {
            // Arrange
            string expected = "..\n..\n..\n..\n..\n..\n";

            // Act
            var board = new Board(6, 2);
            var actual = board.ToString();

            // Assert
            Assert.Equal(expected, actual);
        }
```
We can assume that our board should print out as a series of characters with `\n` newlines after each row.

Notice the `.ToString()` method? That won't do what we'd hope it would do: it'll just return 'Spiral.Board', which isn't very helpful! However, we can _override_ it to do what we're looking for (print a string representation of the board):

```cs
        public override string ToString()
        {
            return "A board.";
        }
```

Put this in your `Board` class and define it to return a string representation of your board so the test passes. There are a few different ways you could make the string you're going to return: a `for` loop would be simplest, but if you're feeling adventurous try playing with LINQ (don't forget to add a `using System.Linq;` statement at the top of the file if you do it this way).