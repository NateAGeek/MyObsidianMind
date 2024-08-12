# Overview
Basic overview of the types from JavaScript and their associated types in TypeScript, basically one-to-one.

## Primitive Types
These are all the primitive types in JavaScript with the same "type" in TypeScript.
- [string](https://developer.mozilla.org/en-US/docs/Glossary/String)
- [number](https://developer.mozilla.org/en-US/docs/Glossary/Number)
- [bigint](https://developer.mozilla.org/en-US/docs/Glossary/BigInt)
- [boolean](https://developer.mozilla.org/en-US/docs/Glossary/Boolean)
- [undefined](https://developer.mozilla.org/en-US/docs/Glossary/Undefined)
- [symbol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)
- [null](https://developer.mozilla.org/en-US/docs/Glossary/Null)
## Arrays
Arrays can be written as implicitly such as `[1, 2, 3]` is `Array<number>` or `number[]`. Where `Array<number>` is the generic typing from the Array interface, fun fact extends the `RelativeIndexable` in node global types.
## Any
`any` is a special type in TypeScript that basically reverts the typing to default JavaScript style, so basically no type checking. Also, it assumes all properties and methods are valid on the type. So you can call methods and reassign types without getting any checking. Really should never be used, but can be to just quickly circumvent type checking for quick coding.

## Type Annotations on Variables
Variables can be inferred their types base on their assignment. However, you can explicitly state their types via declaring after the variable name. `let name: $type = $type_matched_value;`

## Functions
Functions parameters are described with their types, primitive or complex. 
```typescript
function greet(name: string) { // State the type of the parameter here
    console.log("Hello, " + name.toUpperCase() + "! :)")
}
```
This will guard the function parameters from accepting any other type, thus also reducing potential bugs.
#### Return Type Annotations
We can also explicitly state our return type, primitive or complex, too for functions.
```typescript
function get_favorite_number(): number { // Stated return type
    return 42; // This will make sure this is returned type match return value
}
```
#### Anonymous Functions
Anonymous functions will do **contextual typing** where it will infer the type from the call signature of the parent function. For example an array of number, calling the forEach method and passing in the callback function, the parameter passed to the anonymous function should be a number.
```typescript
let numbers: number[] = [1, 2, 3, 4];
numbers.forEach((num) => { // num here is contextually to be type number. Since the signature of the forEach is => forEach(callbackfn: (value: T, index: number, array: T[]) => void, thisArg?: any): void; Where T is the generic type of the array. Aka Array<number>
    console.log(num);
})
```

## Object Types
