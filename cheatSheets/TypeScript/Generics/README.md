# Generic Basics

## Generic Function

```typescript
function identity<T>(arg: T): T {
  return arg;
}

// Usage
let output = identity<string>("Hello, Generics!");
let output2 = identity(42); // Type inference
```

## Generic Interface

```typescript
interface Box<T> {
  value: T;
}

// Usage
let box: Box<number> = { value: 42 };
```

## Generic Class

```typescript
class Container<T> {
  private value: T;

  constructor(value: T) {
    this.value = value;
  }

  getValue(): T {
    return this.value;
  }
}

// Usage
let container: Container<string> = new Container("Generic Container");
let value: string = container.getValue();
```

## Generic Constraints

### Basic Constraint

```typescript
function logLength<T>(arg: T[]): void {
  console.log(arg.length);
}

// Usage
logLength([1, 2, 3]); // 3
logLength(["a", "b"]); // 2
logLength("not an array"); // Error: Property 'length' does not exist on type 'string'.
```

### Extending Interface

```typescript
interface Lengthwise {
  length: number;
}

function logLength<T extends Lengthwise>(arg: T): void {
  console.log(arg.length);
}

// Usage
logLength([1, 2, 3]); // 3
logLength("hello"); // 5
logLength({ length: 10 }); // 10
```

## Generic with Classes

### Generic Class with Constraints

```typescript
class Printer<T extends Printable> {
  print(item: T): void {
    console.log(item.toString());
  }
}

// Usage
interface Printable {
  toString(): string;
}

class Book implements Printable {
  toString(): string {
    return "Book";
  }
}

let bookPrinter = new Printer<Book>();
bookPrinter.print(new Book()); // "Book"
```

### Advanced Generics

### Keyof and Lookup Types

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

let obj = { a: 1, b: "hello", c: true };

let value1: number = getProperty(obj, "a"); // 1
let value2: string = getProperty(obj, "b"); // "hello"
let value3: boolean = getProperty(obj, "c"); // true
```

### Mapped Types

```typescript
type Optional<T> = {
  [P in keyof T]?: T[P];
};

// Usage
interface Person {
  name: string;
  age: number;
}

let optionalPerson: Optional<Person> = { name: "John" };
```

### Conditional Types

```typescript
type NonNullable<T> = T extends null | undefined ? never : T;

// Usage
type NonNullableString = NonNullable<string | null>; // string
```

### Declaration Merging with Generics

```typescript
interface Box<T> {
  value: T;
}

interface Box<T> {
  description: string;
}

// Merged interface
let box: Box<number> = { value: 42, description: "A box containing a number" };
```
