## Overview
Javascript is a language that is both weak typed and also dynamically typed. Meaning that variable typing is not required for the language. This adds flexibility to the language, however, has and can lead to bugs if not correctly approached. TypeScript was introduced to prevent these common errors.
### Weak Typing Example in JavaScript
```javascript
// Define variable example as a value of "hello world" that is of type `string`
let example = "hello world";
// However, since the language is weakly typed, we can assign the variable to a
// new type, and it "just works"
example = 32;
```
### Dynamic Typing Example in JavaScript
```javascript
// Define a variable example that has 32 as a value, a number type
let example = 32
// The + operation will cast the type that best fit, strings have priority fun
// fact, and do concatenation
console.log(example + "3")
```

### Static Type-Checking
TypeScript prevents a lot of these problems by making sure types are know at "compile time", and does a static type-check and then transpiles the code to JavaScript. This prevents possible conflicts and bugs before the code is transpiled for the browser or execution stack.
### Weak Typing Example in TypeScript
```javascript
// Define variable example as a value of "hello world" that is of type `string`
let example: string = "hello world";
// TypeScript will now notifiy at compile time that this variable is being 
// reassigned a different type. Preventing possible issues in code in the future.
example = 32;
```
### Dynamic Typing Example in TypeScript
```javascript
// Define a function with type specific paramaters to prevent issues with dynamic
// typing.
function add(a: number, b: number) { 
    return a + b;
}

console.log(add(2, 3)); // Returns 5 since number + number is valid for function
console.log(add(2, "3")); // Has a compilation error
```

_Note: TypeScript will down level the code to be the most compatible with ES3_

### Strictness
By default TypeScript will not check for potentially `null/undefined` values. There is a strict flag that when `true` will opt into stricter checking. 
#### Strict Rules Enabled when True:
- [`alwaysStrict`](https://www.typescriptlang.org/tsconfig/#alwaysStrict)
- [`strictNullChecks`](https://www.typescriptlang.org/tsconfig/#strictNullChecks)
- [`strictBindCallApply`](https://www.typescriptlang.org/tsconfig/#strictBindCallApply)
- [`strictFunctionTypes`](https://www.typescriptlang.org/tsconfig/#strictFunctionTypes)
- [`strictPropertyInitialization`](https://www.typescriptlang.org/tsconfig/#strictPropertyInitialization)
- [`noImplicitAny`](https://www.typescriptlang.org/tsconfig/#noImplicitAny)
- [`noImplicitThis`](https://www.typescriptlang.org/tsconfig/#noImplicitThis)
- [`useUnknownInCatchVariab`](https://www.typescriptlang.org/tsconfig/#useUnknownInCatchVariables)

The two that the handbook notes is `noImplicitAny` and `strictNullChecks`.
#### noImplicitAny
If the type-checker is not able to infer the types it will fallback to any. This basically is just switching to "JavaScript Style" of parsing the type. With this flag enable, anytime that any is inferred will cause an error on any type that is implicitly any.

#### strictNullChecks
Forces the type-checker to handle cases of `null/undefined` more explicit to to make sure we check for potential issues.

