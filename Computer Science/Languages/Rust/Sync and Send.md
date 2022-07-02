# Overview
Sync and Send are [[Rust Traits]] that are used to maintain synchronous data reference and use across multiple threads. This allows the structures to implement them and work over multiple threads.
## Sync
Are used to mark references safe to share across threads. It does require the reference value, `&T`, to be marked as Send.
