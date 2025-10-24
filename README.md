# typescript
typescript question

## what is typescript ?
1) strongly typed programming language .
2) is javascript with types , add features to js without changing it like interfaces , generics , decorators .
3) detect errors at compilation time without running code.
4) analyze code as you type
5) typescript compiler compile ts code to js code (transpilation) .

## TypeScript Config Files (tsconfig.json):
A tsconfig.json file tells the compiler how to compile your project.
```ts
{
  "compilerOptions": {
    "target": "ES6",
    "module": "commonjs",
    "rootDir": "src",
    "outDir": "dist",
    "strict": true
  },
  "include": ["src"]
}
```
1) rootDir-> Specifies where your TypeScript source files are located.
2) outDir -> Tells TypeScript where to put compiled .js files after transpilation.

## statically typed language:
1) variables type are static once we declare it cannot be changed .
2) type of variable known at compilation time
3) better performance at run time no need to check type dynamically .
4) early error detection .

## dynamically typed language :
1) variables type are dynamic -> can be chnaged .
2) type checking at execution
3) error detection after execution .

## Type annotation
means explicitly specifying the type of a variable, parameter, or function return value in your code — so that the compiler (or type checker) knows exactly what kind of data to expect.

## type annotation looks like when dealing with multidimensional arrays (arrays inside arrays).
```ts
let matrix: number[][] = [
  [1, 2, 3],
  [4, 5, 6],
];
```

## note in js every parameter is optional and return undefined if  no default value and you donot use it .

## When you see a ?  optional parameter: 
before a type (like name?: string), it means that the property or parameter is optional — it may or may not be provided.

## What is a Type Alias?
A type alias is a way to create a new name for a type — basically, you define your own custom type.
```ts
type ID = number;

let userId: ID = 123;  // same as number
```

## What is a Union Type?
Value can be one of several types
```ts
let value: string | number;

value = "Hello"; // ✅ OK
value = 123;     // ✅ OK
value = true;    // ❌ Error (boolean not allowed)
```
## intersection types (&) 
Value must satisfy all types at once
```ts
type Dog = { bark: () => void };
type Cat = { meow: () => void };

type DogCat = Dog & Cat; // both Dog AND Cat at the same time

const hybrid: DogCat = {
  bark: () => console.log("Woof!"),
  meow: () => console.log("Meow!")
};

hybrid.bark(); // 🐶
hybrid.meow(); // 🐱
```

## 🧠 What is a Literal Type? 
A literal type means that a value must be exactly equal to a specific string, number, or boolean — not just any value of that type.
```ts
type DiceRoll = 1 | 2 | 3 | 4 | 5 | 6;

function rollDice(): DiceRoll {
  return 4; // ✅ OK (must return one of 1–6)
}
```
## Tuple:
1) Another sort of array type.
2) Know exactly how many element it contain
3) And what types it contain at specific positions.
```ts
let person: [string, number] = ["Aya", 21];
```
Tuple with Rest Elements:
```ts
type Names = [string, ...string[]];

const group1: Names = ["Aya"];               // ✅ OK
const group2: Names = ["Aya", "Omar", "Lina"]; // ✅ OK
```
So you can have at least one string, and then any number of additional strings.
