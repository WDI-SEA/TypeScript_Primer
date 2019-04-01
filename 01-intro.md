# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) TypeScript

### Learning Objectives
- Describe advantages and disadvantages to using TypeScript
- Identify and use basic types, interfaces and additional typescript cruft
- Understand type inference and declaration
- Configure and use the typescript compiler

___

# Why TypeScript?
- Identify bugs at compile time
- type enforcement in large code bases reduces 
- moaaar

___
# Basic Types
We can get started with TypeScript by adding just a little extra cruft to the JS syntax we know and love. By now, you are all very familiar with the javascript primitives: `string`, `number`, `boolean`. TypeScript makes use of these primitives... and then adds to it!

## Applying Type constraints to variables

In order to apply type constraints to our variables with TypeScript, all we need to do is declare a `type` after the variable name, separated by a colon

```typescript
let myVariable: type = "my value"
```
|Basic Types|   |
|:---------:|---|
| String    | Your run of the mill string type  
| Number    | Can be used with decimal integers and floats as well as hex, octal and binary numbers 
| Boolean   | our old friends `true` and `false`
| Any       | oh my! you're telling me I don't actually have to plan ahead?
| Array     | lets add primitive typings to arrays (syntax may vary!) 
| Tuple     | similar to Arrays--example to follow
| Enum      | Enforce a set of values -- we can use custom `Type`s in many cases
| void      | void def
| null      | null
| undefined | undefined

### `strings`
```typescript
let myString: string = "Hello, World!"
let myTemplateLiteral: string = `"${myString}" is the phrase we always use when learning a new language.`
```

### `numbers`
```typescript
let myInt: number = 3;
let myFloat: number = 6.4;
let myHex: number = 0xf00d;
let myOct: number = 0o744;
let myBin: number = 0b1010;
```

### `boolean`
```typescript
let myBool: boolean = true;
myBool = false;
```

### `any`
When a type is not known or required ahead of time, `any` can be used.
```typescript
let myAny: any = 'what should we throw in here?'
myAny = 7
myAny = true

// all ok!
```
However, if we know that a variable can accept both strings or numbers, TypeScript allows us to plan for this scenario with the `|` operator. (This is called a "Union" type and can be a more advanced technique)

```typescript
let myIndecisiveVar: string | number = 'This is ok!'
myIndecisiveVar = 5 // also ok!
myIndecisiveVar = false // Throws an error
```


### Arrays
TypeScript offers 2 options for enforcing type constraints on an array. 
1. Adding `[]` after a type declaration
2. Using angle brackets and the `Array` generic type
```typescript
let myStrings: string[] = ['Hello','World'];
let myStringArray: Array<string> = ['Hello','Squirrel'];

let myNums: number[] = [9,3,6,12];
let myNumArr: Array<number> = [3,3,3,3,3,3];

let arrayOfAny: any[] = ['what','is','purpose','of','this','array','?!', 2, true, {gross: "yup"}]
```
Be careful when using the angle bracket notation as it can cause conflicts when working with TSX, the TypeScript equivalent of JSX.

### Tuples
>Tuple types allow you to express an array where the type of a fixed number of elements is known, but need not be the same. 

```typescript
let myStringNumTuple: [string, number] = ["Hello", 42];
myStringNumTuple = [42, "Hello"] // ☠️ will throw an error at compile time


// When accessing an element with a known index, the correct type is retrieved:
console.log(myStringNumTuple[0].substr(1)); // OK
console.log(myStringNumTuple[1].substr(1)); // Error, 'number' does not have 'substr'

// When accessing an element outside the set of known indices, a union type is used instead:
myStringNumTuple[3] = "world"; // OK, 'string' can be assigned to 'string | number'

console.log(myStringNumTuple[5].toString()); // OK, 'string' and 'number' both have 'toString'

myStringNumTuple[6] = true; // Error, 'boolean' isn't 'string | number'
```

### Enum
According to the TypeScript docs, Enums allow us to 'give friendly names to a set of numeric values'.

```typescript
enum Color {Green, Red, Blue}
let colorChoice: Color = Color.Green // evaluates to 0
let colorString: string = Color[0] // evaluates to "Green"
```
This little bit of TS compiles to this mess of JavaScript
```js
var Color;
(function (Color) {
    Color[Color["Green"] = 0] = "Green";
    Color[Color["Red"] = 1] = "Red";
    Color[Color["Blue"] = 2] = "Blue";
})(Color || (Color = {}));

var colorChoice = Color.Green; // still evaluates to 0
var colorString = Color[0] // still evaluates to "Green"
```

![WTF](https://media.giphy.com/media/ukGm72ZLZvYfS/giphy.gif)
___
#### Explicit vs Implicit Typing




