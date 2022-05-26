# Overview
Rust has a different style of memory management than C or C++. C tends to allow you to allocate memory via malloc and free, allowing the user to define when memory is allocated and deallocated. C++ tends to use smart allocation that is garbage collected when available.
Rust primary approach is to allow the user to define their variables and keep track of their ownership and scope. The ownership and scope of the variable allows the for the rust compiler to correctly determine when to allocate and deallocate variables when the scope or ownership is no longer in use. 
When it comes to allocation of data, Rust follows a practice of trying to store data on the stack. However, when data is required to be stored on the heap(usually due to dynamically needing allocation) than a pointer(address to value on heap) is stored rather than raw value on stack.

## Scope
Scope is fairly straight forward and is comparable to other languages. Variables are scoped to blocks and blocks are defined with `{}`. 

```rust
{
 //Defining a variable in the scope
 let rust_variable = 10;
 // rust_variable is still being used, so it exists in memory
 let rust_variable_two = rust_variable + 1;
 //Both vars are still in scope, and are being printed
 println!("v1 = {}, v2 = {}", rust_variable, rust_variable_two); 
 // both rust_variable/_two are now not being used, they are dropped by the rust compiler
}
```
# Ownership
Ownership is a concept that is fundamental to Rust and understanding how values from the heap are passed and handled. Values have an ownership, and that ownership changes if there is a reference exchange between variables or functions. When there is a change of ownership the original owner becomes invalid and loses refer ability to the heap value. The new owner then has control of the heap value and its reference. When the ownership of the heap value is not longer needed, out of scope, the value is dropped.

!examples

# Clone & Copy
In context of Ownership the Clone and Copy are important structure implementations built into the [Rust std]. Deriving these implementations onto a structure allows the implementer to state how data should be copy or cloned.

Copying data is a implicit bit wise operation, that direct bit copy of the underlying structure. Also note that if Copy is derived, then Clone must also due to Clone being a super trait to Copy.
```rust
#[derive(Debug, Copy, Clone)] //Need to have clone too, since Clone is a supertrait of Copy
struct Foo {
  cat: i32
}

{
  let x = Foo {
    cat: 42
  };
  let y = x; // Makes a copy of x into y, and both referances are valid, nothing is "barrowed" rather a copy is done.

  println!("x = {:?};", x); // Both will have cat property set to 42
  println!("y = {:?};", y);
}
```

Clone allows for better specification, explicit, control on how data should be copied from structure. Allows for altering or preprocessing of the data before a new instance of the struct is created.
```rust
#[derive(Debug, Copy)] //Need to have clone too, since Clone is a supertrait of Copy
struct Foo {
  cat: i32
}

impl Clone for Foo {
  fn clone(&self) -> Self {
    Foo {
      cat: self.cat * 2 + 4
    }
  }
}

{
  let x = Foo {
    cat: 42
  };
  let y = x; // Makes a copy of x into y, and both referances are 
  let z = y.clone();
    
  println!("x = {:?};", x); // Both will have cat property set to 42
  println!("y = {:?};", y);
  println!("z = {:?};", z); // This will have {cat: 88} since the clone altered it
}
```
