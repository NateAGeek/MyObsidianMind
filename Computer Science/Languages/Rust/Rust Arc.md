# Overview
Arc are thread safe reference counters that keep track of resources until the counter reaches zero. When the counter reaches zero the Arc structure is considered not used and is dropped and the memory is freed. 

Arc's are Thread Safe versions of the Rc type. Since they use Atomic operations to maintain their reference counting and data safety. 

## Weak
Arc Weak pointers are reference tracking that holds a non-owning allocation. These are useful for preventing circular reference on referenced data. Example is when a tree like structure is required, the parents could have a **strong reference** to their children. This would require the parent to have references to the children. The children could have **weak references** to their parents, implying that the parents are allowed to drop and their subsequent children should loose reference to their parents and not force the data to be maintained via strong reference.

## Strong
Strong references are used to keep track if the Arc memory allocation should be maintained. They are used as the counter for if the reference should be dropped. Unlike **weak references** a strong reference counter will determine if the allocated data should be dropped if the number of strong references ever reaches 0.