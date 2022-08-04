Tokio is a runtime for handling async code in Rust.

### Tasks
Tasks are async [[../../../Theory/Green threads|Green Threads]] that execute async functions "separately" (again, green threads) on their own task. They use the `tokio::spawn` to spawn a task that can execute async code. spawns return a JoinHandle that you can await on. These JoinHandle will return a result that you can unwrap.

***'static bound***
Spawned tasks are 'static bound. So they can not contain any data outside their task. To share data across spawns they need to be [[Rust Arc |Arc]] reference so data can be shared and accounted for.


