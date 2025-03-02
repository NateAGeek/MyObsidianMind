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
Are structured types that have properties that describe the data. You can define them as `key: value` pairs or you can further describe them with typing `[key: string]: value_type`. There is also **optional** properties that can be defined via the "?". This is basically an alias for the expected key type and `undefined`.

## Union Types
You can also define types are union of one another, union is basically just a "or" validation of the type (so, `x: number | string` means x can be a number or a string).
#### Working with Union Types
It is useful to better type check possible types for input, however, it is also important to make sure you are calling appropriate methods.
```typescript
function printId(id: number | string) {
    console.log(id.toUpperCase()); // This generates an error since number does not have toUpperCase method.
}
```
A better way to write this is to do a type check of the is to utilize the `typeof` ability of JavaScript.
```typescript
function printId(id: number | string) {
    if (typeof id === "string") { // Type-checker will now have id as a "string" in this block of code
        console.log(id.toUpperCase());
    } else { // This exahustive standpoint of the type will have to be a "number"
        console.log(id);
    }
}
```

## Type Aliases
TypeScript has the `type` keyword, used to assign aliases to types. This can be simple as directly mapping to a primitive type or aliasing to a complex object structure type. 
```typescript
type StringAlias = string;

type ComplexType = {
    hello: string;
    world: string;
    foo: StringAlias;
};
```
## Interfaces
Interfaces are another way to declare an object type, but only object types. 
```typescript
interface ComplexInterface {
    hello: string;
    world: string;
}
```

## Interface vs. Type Alias
Although they are basically all the same, the one key difference is a type alias can only be declared once and not extended. The idea is interfaces can be extended and redefined later with more properties. 
```typescript
interface Example {
  title: string;
}  
interface Example {
  temp: any
}  
const e: Example = {
    title: "hello",
    temp: "temp"
}; // Both properties are valid and accepted
```
While type alias
```typescript
type Example = {
  title: string;
}  
type Example = {
  temp: any
} // Will generate an error since we can not redefine the type or extend the type.
```

## Type Assertions
Asserting the type is sometimes necessary when the return value of something is not clear. For example the `getElementById("cavas_node")` returns a `HTMLElement`, however, if we know the element should be a Canvas, we then have `HTMLCanvasElement` that we can assert via the `as` keyword. 
```typescript
const canvas: HTMLCanvasElement = document.getElementById("cavas_node") as HTMLCanvasElement;
```

#### Double Assertions
Sometimes you might really need to take control of the asserting of a type. That means the type you have might have semi overlap in typing of another type you are trying to assert. 
```typescript
type A = {
    a: number;
    b: string;
};

type B = {
    a: string;
    someStr: string;
};

let a: A = {a: 1, b: "2"};
let b: B = a as unknown as B; // We need to cast to unknown since property "a" overlaps
```
Casting to `unknown` is required since there can be overlap in the types of `A` and `B`. Although this is not good practice. It is an example of taking control of the type-checker, and forcing types that you may have better knowledge of. We need to cast it to `unknown` first because the `unknown` type means it can be any type (but not assignable). So we are casting it basically to anything and then casting it to type `B`. 

## Literal Types
`const` is the only keyword that will force the type to be literally the value.
```typescript
const hello = "world";
// The type of hello is not string, but actually "world". 
```
You can explicitly state fixed types too that are of primitive. For example a function like so:
```typescript
function example(x: "one" | "two" | 3) {
    // x now has to be a literal string of "one", "two", or 3
    console.log(x);
}
console.log(example("one")) //Works
console.log(example(4)) // Fails since for is not leterally "one", "two", or 3
```
To define Objects as literal, you need to provide the `as const` at the end. That will define all the properties as `const` and thus force them to be literal for the type.
```typescript
const req = { url: "https://example.com", method: "GET" } as const;
handleRequest(req.url, req.method); // This now works because method is literal "GET".
```

## null and undefined
`null` and `undefined` are two primitives in JavaScript that TypeScript has as types. However, depending on strict mode or `strictNullChecks` mode on. You will need to test for `null`.

You can bypass this with the `!` **Non-null Assertion Operator** , this will tell the type-checker this can't be `undefined` or `null`. But this is an assumption, not a transpiled check. 
