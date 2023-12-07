# Higher-order functions and lambdas

## Higher-order functions

A higher-order function is a function that takes functions as parameters, or returns a function.

Example:

```kotlin
fun calculate(x: Int, y: Int, operation: (Int, Int) -> Int): Int {
    return operation(x, y);
}

fun sum(x: Int, y: Int) = x + y;

fun main() {
    val data = calculate(30, 50) { a, b -> a * b}
    println(data)
}
```

## Lambda Expression

A lambda expression in Kotlin is a concise, unnamed function enclosed in braces, used for defining code blocks that can be passed as values or stored as variables.

A simple lambda expression

```kotlin
fun main() {
	var myVar = {
        println("Hello I am a simple lambda expression")
    }

    // Method 1
    myvar()

    // Method 2
    myVar.invoke()
}
```

### Syntax of Lambda expression

```kotlin
val lambda_name : Data_type = { argument_List -> code_body }
```

- A lambda expression is always surrounded by curly braces, argument declarations go inside curly braces and have optional type annotations, the code_body goes after an arrow `->` sign.

- If the inferred return type of the lambda is not Unit, then the last expression inside the lambda body is treated as return value.
  Example:
  ```kotlin
  val sum = {a: Int , b: Int -> a + b}
  ```
- In Kotlin, the lambda expression contains optional part except code_body. Below is the lambda expression after eliminating the optional part.
  ```kotlin
  val sum:(Int,Int) -> Int = { a, b -> a + b}
  ```

### Type inference in lambdas

Kotlin’s type inference helps the compiler to evaluate the type of a lambda expression. Below is the lambda expression using which we can compute the sum of two integers.

```kotlin
val sum = {a: Int , b: Int -> a + b}
```

Here, Kotlin compiler self evaluate it as a function which take two parameters of type `Int` and returns `Int` value.

```kotlin
(Int,Int) -> Int
```

Return a String:

```kotlin
val sum1 = { a: Int, b: Int ->
    val num = a + b
    num.toString()     //convert Integer to String
}
```

In the above code, Kotlin compiler self evaluate it as a function which takes two integer values and returns String.

```kotlin
(Int,Int) -> String
```

### Type declaration in lambdas

We must explicitly declare the type of our lambda expression, if lambda returns no value then we can use: `Unit `

Lambdas examples with return type

```kotlin
val lambda1: (Int) -> Int = (a -> a * a)
val lambda2: (String,String) -> String = { a , b -> a + b }
val lambda3: (Int)-> Unit = {print(Int)}
```

### Kotlin program when lambdas used as class extension

```kotlin


val lambda1 : String.(Int) -> String = { this + it }

fun main(args: Array<String>) {
    val result = "Geeks".lambda1(50)
    print(result)
}
```

Output:

```bash
Geeks50
```

### it: implicit name of a single parameter

Example: 1 (using `it`)

```kotlin
val numbers = arrayOf(1,-2,3,-4,5)

fun main(args: Array<String>) {
      println(numbers.filter {  it > 0 })
}
```

Output:

```bash
[1, 3, 5]
```

Example: 2 (Long format)

```kotlin
val numbers = arrayOf(1,-2,3,-4,5)

fun main(args: Array<String>) {
     println(numbers.filter {item -> item > 0 })
}
```
