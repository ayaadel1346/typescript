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

## void Type
A function with return type void runs some code but doesn’t return anything.

## 🔥 never Type 
never means “this function never finishes normally.”
It’s used when a function never returns — for example:
1) It throws an error
2) It runs forever

## 🎯 1. What is an Enum?
Enum (short for “enumeration”) is a TypeScript feature that allows you to define a set of named constants —> used for logical grouping.

```ts
enum Direction {
  Up,      // 0
  Down,    // 1
  Left,    // 2
  Right    // 3
}
```
By default is number based, the first member has value 0, and each following member increments by 1.

Instead of numbers, you can use string values for better readability:
```ts
enum Status {
  Success = "SUCCESS",
  Failure = "FAILURE",
  Pending = "PENDING"
}

let currentStatus: Status = Status.Success;
console.log(currentStatus); // "SUCCESS"
```

⚙️ 3. Heterogeneous Enum
A heterogeneous enum mixes string and numeric members together.
```ts
enum Result {
  Success = 1,
  Failure = "FAILED"
}
```

# 🧩 Type Assertion in TypeScript

## 📘 What is Type Assertion?

Type assertion in TypeScript is a way to **manually tell the compiler** the type of a variable when TypeScript cannot infer it correctly.


## 🧩 Example 1: Basic Example

```ts
let value: unknown = "Hello TypeScript!";

// TypeScript doesn’t know it’s a string until we assert it
let length = (value as string).length;

console.log(length); // ✅ 17
```

Here, `value` was `unknown`, so we had to assert it as a `string` before accessing `.length`.

---

## 🧰 Example 2: HTML Input Element

When selecting elements from the DOM, TypeScript often infers them as a generic `Element` or `HTMLElement`. To access properties specific to certain elements, use **type assertion**.

```ts
// Selecting an input element
const input = document.querySelector('input#username') as HTMLInputElement;

input.value = "Aya Elmahdy";
console.log(input.value); // ✅ "Aya Elmahdy"
```

Without the assertion, TypeScript would not let you access `.value` because not all elements have that property.

---

## 🖼️ Example 3: HTML Image Element

```ts
const img = document.getElementById('profile-pic') as HTMLImageElement;

img.src = 'avatar.png';
img.alt = 'User Profile Picture';
```

Again, `getElementById` returns `HTMLElement | null`, but by asserting it as `HTMLImageElement`, TypeScript allows access to `src` and `alt`.

---

## 🧩 Example 4: Working with Unknown Values

`unknown` is a **safe type** that represents any value — but you cannot use it directly until you assert its type.

```ts
function processData(data: unknown) {
  if (typeof data === 'string') {
    console.log((data as string).toUpperCase()); // ✅ Safe after assertion
  }
}

processData('typescript');
```

### ⚠️ Why use `unknown` with `as`

When you’re unsure of the data type (like from an API or dynamic input), `unknown` prevents unsafe operations until you explicitly check or assert its type.

---


## 🧠 When to Use `as`

Use `as` when:

* TypeScript can’t infer the exact element or object type.
* You’re working with DOM elements (input, image, video, etc.).
* You’re handling values typed as `unknown` or from `any` sources (like API responses).
* You’re narrowing down a union type manually.


---

### 🔍 Example Summary

```ts
// Input element
const nameInput = document.querySelector('#name') as HTMLInputElement;
nameInput.value = 'Aya';

// Image element
const avatar = document.getElementById('avatar') as HTMLImageElement;
avatar.src = 'user.png';

// Working with unknown
let response: unknown = 'Success';
console.log((response as string).toUpperCase());
```

---

# 🧩 Interfaces in TypeScript

## 📘 What is an Interface?

An **interface** in TypeScript is a way to define the **shape of an object** — what properties it should have, their types, and sometimes method signatures. It is a **contract** that objects or classes must follow.

Interfaces help make your code more readable, consistent, and type-safe.

---

## 🧠 Why Use Interfaces?

* To define **object structures** clearly.
* To ensure **type checking** during compile time.
* To promote **code reusability**.
* To define **contracts for classes**.

---

## 🧩 Basic Syntax

```ts
interface Person {
  name: string;
  age: number;
}

const user: Person = {
  name: "Aya Elmahdy",
  age: 22,
};
```

Here, the `user` object must match the structure defined by the `Person` interface.

---

## 🧰 Optional Properties

Use `?` to mark a property as optional:

```ts
interface User {
  username: string;
  email?: string;
}

const user1: User = { username: "Aya" }; // ✅ OK
const user2: User = { username: "Ali", email: "ali@gmail.com" }; // ✅ OK
```

---

## 🧩 Readonly Properties

You can make properties **read-only** using the `readonly` keyword:

```ts
interface Car {
  readonly model: string;
  year: number;
}

const myCar: Car = { model: "Toyota", year: 2023 };
myCar.year = 2024; // ✅ allowed
myCar.model = "Honda"; // ❌ Error: Cannot assign to 'model' because it is a read-only property
```

---

## 🧩 Methods in Interfaces

Interfaces can include **method definitions**:

```ts
interface Animal {
  name: string;
  makeSound(): void;
}

const dog: Animal = {
  name: "Buddy",
  makeSound() {
    console.log("Woof!");
  },
};

dog.makeSound(); // ✅ Woof!
```

---

## 🧩 Extending Interfaces

Interfaces can **extend other interfaces**, allowing reusability and inheritance.

```ts
interface Person {
  name: string;
}

interface Employee extends Person {
  jobTitle: string;
}

const worker: Employee = {
  name: "Aya",
  jobTitle: "Developer",
};
```

This helps you build larger, more structured types without repeating yourself.

---

## 🧩 Interfaces and Functions

You can use interfaces to describe **function types**:

```ts
interface Add {
  (x: number, y: number): number;
}

const addNumbers: Add = (a, b) => a + b;
console.log(addNumbers(5, 3)); // ✅ 8
```

---

## 🧩 Interfaces with Classes

Classes can **implement** interfaces to enforce structure:

```ts
interface Shape {
  getArea(): number;
}

class Circle implements Shape {
  constructor(public radius: number) {}
  getArea(): number {
    return Math.PI * this.radius ** 2;
  }
}

const circle = new Circle(5);
console.log(circle.getArea()); // ✅ 78.5
```

If the class doesn’t implement all properties/methods defined in the interface, TypeScript throws an error.

---

## 🧩 Extending Multiple Interfaces

An interface can extend **multiple other interfaces**:

```ts
interface A {
  a: string;
}

interface B {
  b: string;
}

interface C extends A, B {
  c: string;
}

const obj: C = { a: "Hello", b: "World", c: "!" };
```

---

## 🧠 Difference Between `type` and `interface`

| Feature             | `interface`                     | `type`                               |
| ------------------- | ------------------------------- | ------------------------------------ |
| Extendable          | ✅ Yes                           | ✅ Yes (via intersections)            |
| Declaration merging | ✅ Supported                     | ❌ Not supported                      |
| Suitable for        | Object shapes & class contracts | Unions, primitives, tuples, and more |

Both are often interchangeable for objects, but **interfaces** are better when defining contracts or working with classes.

---





```
So you can have at least one string, and then any number of additional strings.
