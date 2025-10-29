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

# 🔒 Access Modifiers in TypeScript

## 📘 What Are Access Modifiers?

Access modifiers in TypeScript are keywords that **control the visibility** (or accessibility) of class members — properties and methods. They determine where and how a member can be accessed.

There are **three main access modifiers**:

* `public`
* `private`
* `protected`

By default, all class members are **public** if no modifier is specified.

---

## 🧩 1. Public

### 🔹 Definition:

Members declared as `public` are **accessible from anywhere** — inside the class, in subclasses, and outside the class.

### 🔹 Example:

```ts
class Person {
  public name: string;

  constructor(name: string) {
    this.name = name;
  }

  public greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}

const person = new Person('Aya');
console.log(person.name); // ✅ Accessible
person.greet(); // ✅ Accessible
```

### ✅ Use Case:

Use `public` when you want the property or method to be **freely accessible** across your program.

---

## 🧩 2. Private

### 🔹 Definition:

Members declared as `private` are **only accessible within the same class**. They **cannot** be accessed from outside or from subclasses.

### 🔹 Example:

```ts
class Account {
  private balance: number;

  constructor(initialBalance: number) {
    this.balance = initialBalance;
  }

  private calculateInterest() {
    return this.balance * 0.05;
  }

  public showBalance() {
    console.log(`Balance: $${this.balance}`);
  }
}

const account = new Account(1000);
account.showBalance(); // ✅ Accessible
// account.balance; // ❌ Error: 'balance' is private
// account.calculateInterest(); // ❌ Error: 'calculateInterest' is private
```

### ✅ Use Case:

Use `private` for **internal class logic** or **sensitive data** that should not be modified or accessed from outside.

---

## 🧩 3. Protected

### 🔹 Definition:

Members declared as `protected` are **accessible within the same class and its subclasses**, but **not outside** those classes.

### 🔹 Example:

```ts
class Animal {
  protected species: string;

  constructor(species: string) {
    this.species = species;
  }
}

class Dog extends Animal {
  public showSpecies() {
    console.log(`This is a ${this.species}`); // ✅ Accessible inside subclass
  }
}

const dog = new Dog('Golden Retriever');
dog.showSpecies(); // ✅ Accessible
// dog.species; // ❌ Error: 'species' is protected
```

### ✅ Use Case:

Use `protected` when you want **child classes to have access**, but still want to **restrict direct access** from outside.

---

## 🧠 Comparison Table

| Modifier      | Accessible in Same Class | Accessible in Subclass | Accessible Outside Class |
| ------------- | ------------------------ | ---------------------- | ------------------------ |
| **public**    | ✅ Yes                    | ✅ Yes                  | ✅ Yes                    |
| **protected** | ✅ Yes                    | ✅ Yes                  | ❌ No                     |
| **private**   | ✅ Yes                    | ❌ No                   | ❌ No                     |

---

## 🧩 Example: All Modifiers Together

```ts
class Employee {
  public name: string;
  protected department: string;
  private salary: number;

  constructor(name: string, department: string, salary: number) {
    this.name = name;
    this.department = department;
    this.salary = salary;
  }

  public getInfo() {
    console.log(`${this.name} works in ${this.department}`);
  }

  private showSalary() {
    console.log(`Salary: ${this.salary}`);
  }
}

class Manager extends Employee {
  constructor(name: string, department: string, salary: number) {
    super(name, department, salary);
  }

  public display() {
    // console.log(this.salary); // ❌ Cannot access private member
    console.log(`Department: ${this.department}`); // ✅ Protected accessible here
  }
}

const emp = new Manager('Aya', 'Development', 5000);
emp.getInfo(); // ✅ Public method
emp.display(); // ✅ Access protected via subclass
// emp.department; // ❌ Error: protected
// emp.salary; // ❌ Error: private
```

---

## ✅ Summary

| Keyword       | Visibility                            | Typical Use                                    |
| ------------- | ------------------------------------- | ---------------------------------------------- |
| **public**    | Accessible everywhere                 | Commonly used for open APIs or public methods  |
| **protected** | Accessible in class + subclasses      | Use for inherited properties or internal logic |
| **private**   | Accessible only inside the same class | Use for sensitive or internal data             |

---

**In short:**

* `public` → open access
* `protected` → access for subclasses only
* `private` → class-only access

These modifiers make your code **more secure, maintainable, and well-structured**.


# ⚙️ Getters and Setters in TypeScript

## 📘 What Are Getters and Setters?

**Getters (`get`)** and **Setters (`set`)** are **special methods** in a class that control how we **read** and **update** the value of private or protected properties.

They allow **encapsulation** — meaning we can hide internal data and provide **controlled access** to it instead of allowing direct modification.

---

## 🧩 Why Use `get` and `set` Instead of `public`

If a property is marked `public`, anyone can directly read or modify it from outside the class.

That can lead to **uncontrolled changes** and break program logic.

Using **private properties** with `get` and `set` gives you:

* 🔒 **Encapsulation** – hide internal details.
* ✅ **Validation** – check or transform data before saving.
* 🔄 **Consistency** – run additional logic when data changes.
* 📦 **Read-only** or **write-controlled** access.

---

## 🧠 Basic Example: Without Getters/Setters

```ts
class User {
  public name: string;
}

const user = new User();
user.name = "Aya"; // ✅ Works
console.log(user.name); // ✅ Aya

// But anyone can set anything, even invalid data
user.name = ""; // ❌ no validation — risky
```

Here, we can’t control what value is assigned to `name`.

---

## 🧩 Example with `get` and `set`

```ts
class User {
  private _name: string = "";

  // Getter - allows controlled read access
  get name(): string {
    return this._name;
  }

  // Setter - allows controlled write access
  set name(value: string) {
    if (value.trim().length === 0) {
      throw new Error("Name cannot be empty");
    }
    this._name = value;
  }
}

const user = new User();
user.name = "Aya Elmahdy"; // ✅ Uses setter
console.log(user.name); // ✅ Uses getter, prints "Aya Elmahdy"

// user._name = ""; // ❌ Error: Property '_name' is private
```

### 🔍 What Happened:

* The property `_name` is **private** — can’t be accessed directly.
* We read `name` using the **getter** (`get name()`)
* We write to `name` using the **setter** (`set name(value)`)
* Validation ensures we can’t assign an invalid value.

---

## 🧩 Example: Using `get` for Derived Values

You can use a **getter** to calculate or transform data before returning it:

```ts
class Rectangle {
  constructor(private _width: number, private _height: number) {}

  get area(): number {
    return this._width * this._height;
  }
}

const rect = new Rectangle(10, 5);
console.log(rect.area); // ✅ 50 (calculated via getter)
```

> The `area` property looks like a normal property but is actually computed dynamically using the getter.

---

## 🧩 Example: Using `set` for Updates

```ts
class BankAccount {
  private _balance: number = 0;

  get balance(): number {
    return this._balance;
  }

  set balance(amount: number) {
    if (amount < 0) throw new Error("Balance cannot be negative");
    this._balance = amount;
  }
}

const account = new BankAccount();
account.balance = 1000; // ✅ set
console.log(account.balance); // ✅ get → 1000

// account.balance = -200; // ❌ Throws error
```

The setter ensures that balance can’t be set to a negative number.

---

## 🧩 Getters and Setters in Action (Update Example)

```ts
class Product {
  private _price: number = 0;

  get price(): number {
    return this._price;
  }

  set price(value: number) {
    if (value < 0) throw new Error("Price cannot be negative");
    console.log(`Price updated from ${this._price} → ${value}`);
    this._price = value;
  }
}

const item = new Product();
item.price = 20; // ✅ Logs: Price updated from 0 → 20
console.log(item.price); // ✅ 20
```

> The `set` method allowed validation **and** triggered a log message when the property changed.

---

## 🧠 Why Use `private` with Getters and Setters

* Keeps internal data **safe from direct access**.
* Forces external code to use `get`/`set`, where you can control behavior.
* Makes your class more **robust** and **maintainable**.

---

## 🧩 Summary

| Feature       | Description                                                |
| ------------- | ---------------------------------------------------------- |
| **`get`**     | Used to read a private property’s value safely             |
| **`set`**     | Used to update a private property with validation or logic |
| **`private`** | Restricts direct access to class members                   |
| **Benefit**   | Encapsulation, validation, computed values, logging        |

---

### ✅ Example Summary

```ts
class UserProfile {
  private _email: string = "";

  get email(): string {
    return this._email.toLowerCase(); // Transform before returning
  }

  set email(value: string) {
    if (!value.includes('@')) throw new Error('Invalid email');
    this._email = value;
  }
}

const profile = new UserProfile();
profile.email = 'AYA@MAIL.COM'; // set → validation + update
console.log(profile.email); // get → aya@mail.com
```

---

# 📘 Static Members in TypeScript

## 🔹 What Are Static Members?

In TypeScript (and JavaScript), **static members** are **properties or methods** that belong to the **class itself**, not to instances of the class.

That means:

* You **don’t need to create an object** to access a static member.
* You access it **directly through the class name**.

```ts
class MathUtils {
  static PI = 3.14159;

  static calculateArea(radius: number): number {
    return this.PI * radius * radius;
  }
}

console.log(MathUtils.PI); // ✅ Access via class
console.log(MathUtils.calculateArea(5)); // ✅ Access via class
```

> ❌ You **cannot** access static members through an instance:
>
> ```ts
> const m = new MathUtils();
> console.log(m.PI); // ❌ Error
> ```

---

## 🔹 Why Use Static Members?

Static members are useful when:

* The data or function is **shared across all instances**.
* You don’t want each object to duplicate the same logic or data.
* You need **utility functions** or **constants**.

Examples:

* Utility classes (`Math`, `Date`, etc.)
* Shared counters or configuration values.

---

## 🔹 Static vs Instance Members

| Feature     | Static Member              | Instance Member         |
| ----------- | -------------------------- | ----------------------- |
| Belongs To  | Class itself               | Instance (object)       |
| Accessed By | Class name                 | Object reference        |
| Shared?     | Yes, shared among all      | No, unique per instance |
| Use Case    | Utility methods, constants | Object-specific data    |

---

## 🔹 Example with Both Static and Instance Members

```ts
class User {
  private static userCount = 0; // shared counter
  public name: string;

  constructor(name: string) {
    this.name = name;
    User.userCount++; // Access static via class name
  }

  static getUserCount(): number {
    return User.userCount;
  }
}

const u1 = new User("Aya");
const u2 = new User("Omar");

console.log(User.getUserCount()); // 2 ✅ shared across all users
```

---

## 🔹 Why Use `static` Instead of `public` Instance Members?

If you used a `public` property instead:

* Each instance would have its own **copy**.
* You’d waste memory and possibly cause inconsistency.

Using `static` ensures one **shared source of truth**.

---

## 🔹 Real-World Example

```ts
class Config {
  static API_URL = "https://api.example.com";

  static log(message: string): void {
    console.log(`[LOG] ${message}`);
  }
}

Config.log(`Connecting to ${Config.API_URL}`);
```

---

## 🔹 Summary

* `static` → Belongs to the class, not objects.
* Access using `ClassName.member`.
* Useful for shared data or utility methods.
* Reduces duplication and improves consistency.

**Use static members when behavior or data is not tied to individual instances but to the class as a whole.**


---
# 📘 Abstract Classes and Members in TypeScript

## 🔹 What Is an Abstract Class?

An **abstract class** in TypeScript is a **blueprint** for other classes.

* It **cannot be instantiated** directly.
* It may contain **abstract methods** (methods with no implementation).
* It may also contain **normal (concrete)** methods and properties.

You use an abstract class when you want to **define a common structure or behavior** that derived classes must follow.

---

## 🧩 Example: Basic Abstract Class

```ts
abstract class Animal {
  // Abstract method (must be implemented by subclasses)
  abstract makeSound(): void;

  // Concrete method (optional shared implementation)
  move(): void {
    console.log("The animal moves");
  }
}

class Dog extends Animal {
  makeSound(): void {
    console.log("Woof! Woof!");
  }
}

const dog = new Dog();
dog.makeSound(); // Woof! Woof!
dog.move();      // The animal moves

// const animal = new Animal(); // ❌ Error: Cannot create an instance of an abstract class
```

---

## 🔹 Abstract Members

An **abstract member** (method or property):

* Is declared using the `abstract` keyword.
* Has **no implementation** in the base class.
* **Must** be implemented in the derived class.

```ts
abstract class Shape {
  abstract area(): number;
  abstract perimeter(): number;
}

class Rectangle extends Shape {
  constructor(private width: number, private height: number) {
    super();
  }

  area(): number {
    return this.width * this.height;
  }

  perimeter(): number {
    return 2 * (this.width + this.height);
  }
}

const rect = new Rectangle(10, 5);
console.log(rect.area());      // 50
console.log(rect.perimeter()); // 30
```

---

## 🔹 Why Use Abstract Classes?

Use abstract classes when you want to:

1. **Force subclasses** to implement specific methods.
2. Provide a **base structure** or **shared behavior**.
3. Encourage **consistency** among related classes.

For example:

```ts
abstract class Database {
  abstract connect(): void;
  abstract disconnect(): void;

  logStatus(): void {
    console.log("Database status checked.");
  }
}

class MySQLDatabase extends Database {
  connect(): void {
    console.log("Connected to MySQL database.");
  }
  disconnect(): void {
    console.log("Disconnected from MySQL database.");
  }
}

const db = new MySQLDatabase();
db.connect();
db.logStatus();
db.disconnect();
```

---

## 🔹 Abstract Properties

You can also define **abstract properties** that must be provided by subclasses.

```ts
abstract class Person {
  abstract name: string;
  abstract age: number;

  greet(): void {
    console.log(`Hello, my name is ${this.name}`);
  }
}

class Employee extends Person {
  name = "Aya";
  age = 25;
}

const emp = new Employee();
emp.greet(); // Hello, my name is Aya
```

---

## 🔹 Abstract Class vs Interface

| Feature                     | Abstract Class          | Interface                   |
| --------------------------- | ----------------------- | --------------------------- |
| Can have implementations?   | ✅ Yes                   | ❌ No                        |
| Can have fields/properties? | ✅ Yes                   | ✅ Yes                       |
| Can be instantiated?        | ❌ No                    | ❌ No                        |
| Inheritance                 | Only one abstract class | Multiple interfaces         |
| Use case                    | Common base with logic  | Shape of object / structure |

Example:

```ts
interface Flyable {
  fly(): void;
}

abstract class Bird {
  abstract sound(): void;
  move(): void {
    console.log("Bird is flying");
  }
}

class Sparrow extends Bird implements Flyable {
  sound(): void {
    console.log("Chirp chirp");
  }
  fly(): void {
    console.log("Sparrow flies high");
  }
}
```

---

## 🔹 Summary

* `abstract` classes define **templates** for subclasses.
* Abstract members **must** be implemented in derived classes.
* They can mix **implemented (concrete)** and **unimplemented (abstract)** logic.
* Use abstract classes when you want to **enforce structure and share behavior** at the same time.

# 📘 Polymorphism and `override` Modifier in TypeScript (Easy Explanation)

## 🔹 What is Polymorphism?

**Polymorphism** means *many forms*. It allows a parent class to have many child classes that can use the same method name but do **different actions**.
---

## 🐾 Example

```ts
class Animal {
  makeSound(): void {
    console.log("Some sound");
  }
}

class Dog extends Animal {
  override makeSound(): void {
    console.log("Woof!");
  }
}

class Cat extends Animal {
  override makeSound(): void {
    console.log("Meow!");
  }
}

const animals: Animal[] = [new Dog(), new Cat(), new Animal()];

for (const a of animals) {
  a.makeSound();
}
// Output:
// Woof!
// Meow!
// Some sound
```

🧠 **Explanation:** All animals share the same method name (`makeSound`), but each gives a different result depending on its class.

---

## 🔹 Why Use Polymorphism?

* You can use **one function** to work with **different objects**.
* It makes your code **cleaner and easier to extend**.
* You don’t have to rewrite the same logic for each type.
---

## 🔹 What is the `override` Modifier?

When a child class changes a method that already exists in the parent class, it’s called **overriding**.

The **`override` keyword** helps TypeScript check that:

* The method actually exists in the parent.
* You didn’t make a typo by mistake.

Example:

```ts
class Vehicle {
  start(): void {
    console.log("Starting vehicle...");
  }
}

class Car extends Vehicle {
  override start(): void { // overriding the parent method
    console.log("Car engine started!");
  }
}

const myCar = new Car();
myCar.start(); // Car engine started!
```

If you write it wrong:

```ts
class Bike extends Vehicle {
  override strat(): void { // ❌ Error: no method 'strat' in parent
    console.log("Bike started!");
  }
}
```

The `override` keyword catches the mistake!

---

## 🔹 Using `super`

Sometimes you want to use the parent method **and** add extra code. You can call the parent version using `super`.

```ts
class Parent {
  greet(): void {
    console.log("Hello from Parent");
  }
}

class Child extends Parent {
  override greet(): void {
    super.greet(); // Call parent method
    console.log("Hello from Child");
  }
}

const c = new Child();
c.greet();
// Output:
// Hello from Parent
// Hello from Child
```

---

## 🔹 Real-World Example

```ts
abstract class Payment {
  abstract pay(amount: number): void;
}

class CreditCard extends Payment {
  override pay(amount: number): void {
    console.log(`Paid ${amount} using Credit Card`);
  }
}

class PayPal extends Payment {
  override pay(amount: number): void {
    console.log(`Paid ${amount} using PayPal`);
  }
}

const payments: Payment[] = [new CreditCard(), new PayPal()];
for (const p of payments) {
  p.pay(100);
}
// Output:
// Paid 100 using Credit Card
// Paid 100 using PayPal
```

---

## 🔹 Summary

| Concept          | Meaning                                            |
| ---------------- | -------------------------------------------------- |
| **Polymorphism** | Same method name, different behavior in each class |
| **Override**     | Used when redefining a parent method in the child  |
| **Super**        | Used to call the parent’s version of a method      |


# TypeScript Generics

## 🧩 What Are Generics?

Generics in TypeScript allow you to create reusable and flexible code by writing functions, classes that can work with **any data type**. Instead of fixing a type, generics use a **type variable** (like `<T>`) that gets replaced when the code is used.

### 🧠 Why Use Generics?

* To make code **reusable** for different data types.
* To maintain **type safety**.
* To avoid using `any`, which disables type checking.

---

## 🧮 1. Basic Generic Example

```ts
function identity<T>(value: T): T {
  return value;
}

// Usage
let num = identity<number>(10); // T = number
let str = identity<string>("Hello"); // T = string
```

Here `T` is a type placeholder. When you call the function, TypeScript infers the type automatically.

---

## ⚙️ 2. Generic with Functions

Generics help create functions that can handle different types safely.

```ts
function getFirstElement<T>(arr: T[]): T {
  return arr[0];
}

const numbers = getFirstElement<number>([1, 2, 3]); // number
const names = getFirstElement<string>(["Aya", "Sara"]); // string
```

This function works with any array type.

---

## 🧱 3. Generic with Classes

You can make a class generic by adding `<T>` after the class name.

```ts
class Box<T> {
  private content: T;

  constructor(value: T) {
    this.content = value;
  }

  getValue(): T {
    return this.content;
  }
}

const numberBox = new Box<number>(100);
console.log(numberBox.getValue()); // 100

const stringBox = new Box<string>("TypeScript");
console.log(stringBox.getValue()); // TypeScript
```

Each `Box` instance can store a specific type.

---

## 🔁 4. Multiple Generics

You can use more than one type variable.

```ts
function pair<T, U>(first: T, second: U): [T, U] {
  return [first, second];
}

const mixed = pair<string, number>("Age", 25);
console.log(mixed); // ["Age", 25]
```

Here we used `<T, U>` to allow two different types.

---

## ⚙️ 5. Default Generic Type

You can set a **default type** for a generic parameter.

```ts
function showData<T = string>(data: T): T {
  return data;
}

console.log(showData("Aya")); // Aya
console.log(showData<number>(25)); // 25
```

If no type is provided, `T` defaults to `string`.

---


```ts
interface UserInfo {
  name: string;
  age: number;
}

class DataStore<T> {
  private data: T;

  constructor(value: T) {
    this.data = value;
  }

  getData(): T {
    return this.data;
  }
}


const userStore = new DataStore<UserInfo>({ name: "Aya", age: 22 });
console.log(userStore.getData()); // { name: "Aya", age: 22 }
```


---

## 🧠 Summary

| Concept           | Description                                  | Example                          |
| ----------------- | -------------------------------------------- | -------------------------------- |
| Generic Function  | Works with any type                          | `function identity<T>(value: T)` |
| Generic Class     | Reusable class with flexible type            | `class Box<T>`                   |
| Multiple Generics | Use more than one type variable              | `<T, U>`                         |
| Default Type      | Provides fallback type                       | `<T = string>`                   |
---



