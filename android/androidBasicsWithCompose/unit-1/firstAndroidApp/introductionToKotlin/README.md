# Kotlin Basics

## Functions

```kotlin
fun main() {
    println("Hello, world!")
}
```

- A Kotlin program requires a main function as the entry point of the program.
- To define a function in Kotlin, use the `fun` keyword, followed by the name of the function, any inputs enclosed in parentheses, followed by the function body enclosed in curly braces.
- The name of a function should follow camel case convention and start with a lowercase letter.
- Use the `println()` function call to print some text to the output.
- Refer to the Kotlin style guide for formatting and code conventions to follow when coding in Kotlin.
- Troubleshooting is the process of resolving errors in your code.

### The Unit type

By default, if you don't specify a return type, the default return type is `Unit`. `Unit` means the function doesn't return a value. `Unit` is equivalent to void return types in other languages (`void` in Java and C; `Void/empty tuple ()` in Swift; `None` in Python, etc.). Any function that doesn't return a value implicitly returns `Unit`. You can observe this by modifying your code to return `Unit`.

```kotlin
fun main() {
    birthdayGreeting()
}

fun birthdayGreeting(): Unit {
    println("Happy Birthday, Rover!")
    println("You are now 5 years old!")
}
```

### Parameters

```kotlin
fun birthdayGreeting(name: String): String {
    val nameGreeting = "Happy Birthday, Rover!"
    val ageGreeting = "You are now 5 years old!"
    return "$nameGreeting\n$ageGreeting"
}
```

### Multiple Parameters

```kotlin
fun birthdayGreeting(name: String, age: Int): String {
    val nameGreeting = "Happy Birthday, $name!"
    val ageGreeting = "You are now $age years old!"
    return "$nameGreeting\n$ageGreeting"
}
```

### Function Signature

The function name with its inputs (parameters) are collectively known as the function signature.

### Default Arguments

```kotlin
fun birthdayGreeting(name: String = "Rover", age: Int): String {
    return "Happy Birthday, $name! You are now $age years old!"
}
```

## Variables

### Kotlin data type

- String - Text - "Add contact", "Search", "Sign in"
- Int - Integer number - 32, 1293490, -59281
- Double - Decimal number - 2.0, 501.0292, -31723.99999
- Float - Decimal number (that is less precise than a Double). Has an f or F at the end of the number. - 5.0f, -1630.209f, 1.2940278F
- Boolean - true or false

### Examples

```kotlin
    val count: Int = 2
    println("You have $count unread messages.")
```

### Type inference

Type inference is when the Kotlin compiler can infer (or determine) what data type a variable should be, without the type being explicitly written in the code.

```kotlin
val count = 2
```

### Basic math operations

```kotlin
fun main() {
    val unreadCount = 5
    val readCount = 100
    println("You have ${unreadCount + readCount} total messages in your inbox.")
}
```

### Update variables

```kotlin
fun main() {
    val cartTotal = 0 // Compilation Error
    cartTotal = 20
    println("Total: $cartTotal")
}
```

- The `val cartTotal` can't be reassigned to another value (`20`) after it's been assigned an initial value (`0`).

* `val` keyword - Use when you expect the variable value will not change.
* `var` keyword - Use when you expect the variable value can change.
