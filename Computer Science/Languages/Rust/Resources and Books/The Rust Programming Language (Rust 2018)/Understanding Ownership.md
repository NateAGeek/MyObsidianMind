# Overview
Rust has a different style of memory management than C or C++. C tends to allow you to allocate memory via malloc and free, allowing the user to define when memory is allocated and deallocated. C++ tends to use smart allocation that is garbage collected when available.

Rust primary approach is to allow the user to define their variables and keep track of their ownership and scope. The ownership and scope of the variable allows the for the rust compiler to correctly determine when to allocate and deallocate variables when the scope or ownership is no longer in use. 

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

