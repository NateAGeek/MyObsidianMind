# Overview
Defining enums is fairly straight forward. You can also add details of the structure of the enum by passing a structure or type.
They allow nested passing of other enums and types. This can be useful for creating a semi functional tree of structs, and can lead to really useful matching on data. Mixed in with `ref` and other techniques can allow for the proper extraction of data in a define enum structure. 

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