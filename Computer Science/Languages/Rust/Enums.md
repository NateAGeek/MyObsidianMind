# Overview
Defining enums is fairly straight forward. You can also add details of the structure of the enum by passing a structure or type.

```rust
#[derive(Debug)]
enum HelloWorld {
  Hello,
  World,
  Param(String)
}

fn main() {
  let hello = HelloWorld::Hello;
  let world = HelloWorld::World;
  let param = HelloWorld::Param(String::from("Hello a Param!"));
  let param2 = HelloWorld::Param(String::from("Hello a Param2!"));

  println!("{:?}", hello);
  println!("{:?}", world);
  println!("{:?}", param);
  println!("{:?}", param2);
}
```