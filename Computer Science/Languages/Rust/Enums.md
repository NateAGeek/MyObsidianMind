# Overview
Defining enums is fairly straight forward. You can also add details of the structure of the enum by passing a structure or type.

```rust
enum Example {
    Hello,
    World
}
let t = Example::Hello;
```

```rust
enum Example2 {
    Hello(String),
    World(String)
}
let t = Hello(String::from("Helo"));
```