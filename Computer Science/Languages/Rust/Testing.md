# Overview
To only include tests during testing mode, you need to define a mod with `#[cfg(test)]`

Then to define a test function you need to add the test macro `#[test]` this allows the test to run when you run the `cargo test` command.

**TryBuild**
Is a useful test harness for determining if tests pass, builds pass, and overall macros work.