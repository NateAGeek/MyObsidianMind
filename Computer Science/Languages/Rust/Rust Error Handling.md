### Propagation
Function needs to return a `Result` to handle the `?` operator. This allows you to propagate the error upstream to the caller function. Also, to handle general errors you need to state a dynamic Error Box allocation. This will covert any operation that can error.
```rust
fn possible_issues() -> Result<(), Box<dyn std::error::Error>> {
    //Now we can do anything we want and use the short hand ? operation
}
```