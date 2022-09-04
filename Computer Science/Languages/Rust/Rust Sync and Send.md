# Overview
Sync and Send are [[Rust Traits]] that are used to maintain synchronous data reference and use across multiple threads. This allows the structures to implement them and work over multiple threads.
## Sync
Are used to mark references safe to share across threads. It does require the reference value, `&T`, to be marked as Send.

### Executor
Executors are runtimes that can run async/await futures. They are used to implement proper threading management and typically implement sync -> async features like IO, fs, and network 

## Runtimes
[[Crates/Tokio Crate|Tokio]] is a runtime that appears to be the most popular. It allows rust to run async functions and provides some async implementations of std.
