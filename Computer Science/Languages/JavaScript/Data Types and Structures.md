## Typing Relations: Dynamic vs Weak Typing
JavaScript is both a dynamic and weak typed language. This allows for the dynamics of the value to be reset to any type and any point in the program.
```javascript
let foo = 32;
foo = "32"
console.log(typeof foo === "string") // logs: true
```
Also the language is weakly typed. So, that means the language is designed to try and convert or relate types when best fit, Although this can be nice, it does lead to some moments of unexpected behaviors, classic javascript.
```javascript
const foo = 42;
const result = foo + "1";
console.log(result) // So, the language converts the 42 to a string to properly do the addition operation on string, leadig to print "421"
```

## Primitive Value
In JavaScript and are immutable values are at the lowest level of the language.  `Objects` are a special type that is not immutable and more complex than the primitive types. 

### Null
`null` is the absence of an object. Not to be confused with `undefined` meaning the absence of value. `null` is more defined by the user to give better context of the lack of object value being returned.
### Undefined
Indicates the absence of a value. 


