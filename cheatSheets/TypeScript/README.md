# TypeScript Cheat Sheet

## Basic Types

```typescript
// Boolean
let isDone: boolean = false;

// Number
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;

// String
let color: string = "blue";

// Array
let list: number[] = [1, 2, 3];
let fruits: Array<string> = ["apple", "banana"];

// Tuple
let x: [string, number];
x = ["hello", 10];

// Enum
enum Color {
  Red,
  Green,
  Blue,
}
let c: Color = Color.Green;

// Any
let notSure: any = 4;
notSure = "maybe a string";

// Void
function logMessage(): void {
  console.log("This is a log message");
}

// Null and Undefined
let u: undefined = undefined;
let n: null = null;
```

## Variable Declarations

```typescript
// Let and Const
let variable1: number = 10;
const constant1: string = "immutable";

// Destructuring
let [a, b] = [1, 2];
let { x, y } = { x: 1, y: 2 };
```

## Functions

```typescript
// Function Declaration
function add(x: number, y: number): number {
return x + y;
}

// Arrow Functions
let multiply = (x: number, y: number): number => x \* y;

// Optional and Default Parameters
function greet(name: string, greeting: string = "Hello") {
console.log(`${greeting}, ${name}!`);
}
```

## Interfaces

```typescript
// Interface
interface Person {
  firstName: string;
  lastName: string;
}

function greeter(person: Person) {
  return `Hello, ${person.firstName} ${person.lastName}`;
}

// Class implementing an interface
class Student implements Person {
  firstName: string;
  lastName: string;
  constructor(firstName: string, lastName: string) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
}
```

## Classes

```typescript
// Class
class Animal {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
  makeSound(): void {
    console.log("Generic animal sound");
  }
}

// Inheritance
class Dog extends Animal {
  makeSound(): void {
    console.log("Woof!");
  }
}
```

## Generics

```typescript
// Generic Function
function identity<T>(arg: T): T {
  return arg;
}

// Generic Interface
interface Box<T> {
  value: T;
}

// Generic Class
class Container<T> {
  private value: T;
  constructor(value: T) {
    this.value = value;
  }
}
```

## Enums

```typescript
// Numeric Enum
enum Direction {
  Up = 1,
  Down,
  Left,
  Right,
}

// String Enum
enum Color {
  Red = "RED",
  Green = "GREEN",
  Blue = "BLUE",
}
```

## Type Assertions

```typescript
let someValue: any = "this is a string";
let strLength: number = (someValue as string).length;

// OR

let strLength: number = (<string>someValue).length;
```

## Modules

```typescript
// Exporting
export const variable1: number = 10;

// Importing
import { variable1 } from "./module";
```

## TypeScript Compiler Configuration (tsconfig.json)

```json
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "moduleResolution": "node",
    "baseUrl": "./src",
    "outDir": "./dist",
    "sourceMap": true
  },
  "include": ["src/**/*.ts"],
  "exclude": ["node_modules"]
}
```
