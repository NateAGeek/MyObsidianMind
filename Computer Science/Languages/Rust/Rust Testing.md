# Overview
To only include tests during testing mode, you need to define a mod with `#[cfg(test)]`

Then to define a test function you need to add the test macro `#[test]` this allows the test to run when you run the `cargo test` command.

**TryBuild**
Is a useful test harness for determining if tests pass, builds pass, and overall macros work.

**Tests in other files**
I'd like to put other tests in other files but still keep the ability in other folders. That is kinda against spec, but I don't like the spec. 

```rust
//file: cool_code.rs

//Cool code goes here
fn cool_code() -> &'static str {
    "Cool code bois"
}

#[cfg(test)]
#[path = "./cool_code.tests.rs"]
mod cool_code_tests;
```

