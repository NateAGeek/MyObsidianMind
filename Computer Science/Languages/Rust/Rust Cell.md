# Overview
Cells are used to share data across many accessors but not make it directly mutable.

So a Cell can contain a number, and when the `get` function is called it returns a **Copy** of the value. This allows the ability to move the value around. However, you can also set the value later with `update` this allows the cell to properly update that said value now for future `get` copies.


## Resources
https://www.youtube.com/watch?v=8O0Nt9qY_vo