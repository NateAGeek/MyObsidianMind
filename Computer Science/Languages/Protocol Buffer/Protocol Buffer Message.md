## Basic Message
Messages are the bread and butter of Protocol Buffer. They are the defined schemas that define the structure of the data that is being sent and received.

The basis is that messages consist of a defined message struct with keys and the associated types of data to be sent or received. These fields need to specify a number that will represent the identity in the binary encoding process(compression id of the data). Note, 1-15 ids are only one byte in space of the encoding. 16-2047 take two bytes 

```protobuf
message {
    string hello = 1 // A string that is key by "hello" and its id is 1
    uint32 world = 2 // A unsigned 32 int that is key by "world" and its id is 2
}
```

### Optional
Fields can be labeled at `optional` to allow the data not to be required in the message. You can also specify a default value via `[default = "default_value"]`

```protobuf
message {
    optional string temp = 1 [default = "test"]
}
```

### Required
Fields can also be required. TODO: Need to make sure this is not just a proto2 thing.

### Types
Types | Notes
----- | -----
double | Notes
float | Notes
int32 | Notes
int64 | Notes
uint32 | Notes
uint64 | Notes
sint32 | Notes
sint64 | Notes
fixed32 | Notes
fixed64 | Notes
sfixed32 | Notes
sfixed64 | Notes
bool | Notes
string | Notes
bytes | Notes


