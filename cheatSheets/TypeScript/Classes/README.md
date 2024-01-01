# Classes

## Class Declaration

```typescript
class Animal {
  // Properties
  name: string;
  age: number;

  // Constructor
  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  // Method
  makeSound(): void {
    console.log("Generic animal sound");
  }
}
```

## Class Instances

```typescript
// Creating an instance
const myAnimal = new Animal("Buddy", 3);

// Accessing properties
console.log(myAnimal.name); // Buddy
console.log(myAnimal.age); // 3

// Calling methods
myAnimal.makeSound(); // Generic animal sound
```

## Inheritance

```typescript
class Dog extends Animal {
  // Additional property
  breed: string;

  // Constructor with super
  constructor(name: string, age: number, breed: string) {
    super(name, age);
    this.breed = breed;
  }

  // Overriding parent method
  makeSound(): void {
    console.log("Woof!");
  }

  // New method
  bark(): void {
    console.log("Barking!");
  }
}
```

## Creating an Instance of the Subclass

```typescript
const myDog = new Dog("Max", 2, "Labrador");

console.log(myDog.name); // Max
console.log(myDog.age); // 2
console.log(myDog.breed); // Labrador

myDog.makeSound(); // Woof!
myDog.bark(); // Barking!
```

## Access Modifiers

```typescript
class Person {
  private id: number;
  protected email: string;

  constructor(id: number, email: string) {
    this.id = id;
    this.email = email;
  }
}
```

- `private`: Can only be accessed within the class.
- `protected`: Can be accessed within the class and its subclasses.

## Getter and Setter

```typescript
class Rectangle {
  private _width: number;
  private _height: number;

  constructor(width: number, height: number) {
    this._width = width;
    this._height = height;
  }

  // Getter
  get width(): number {
    return this._width;
  }

  // Setter
  set width(value: number) {
    if (value > 0) {
      this._width = value;
    } else {
      console.error("Width must be greater than 0");
    }
  }

  // Another getter
  get area(): number {
    return this._width * this._height;
  }
}
```

## Static Members

```typescript
class MathOperations {
  static PI: number = 3.14159;

  static calculateCircumference(radius: number): number {
    return 2 * this.PI * radius;
  }
}

console.log(MathOperations.PI); // 3.14159
console.log(MathOperations.calculateCircumference(5)); // 31.4159
```

## Abstract Classes

```typescript
abstract class Shape {
  abstract calculateArea(): number;

  display(): void {
    console.log("This is a shape.");
  }
}

class Circle extends Shape {
  constructor(private radius: number) {
    super();
  }

  calculateArea(): number {
    return Math.PI * this.radius ** 2;
  }
}
```

- Abstract classes cannot be instantiated directly.
- Subclasses must implement abstract methods.
