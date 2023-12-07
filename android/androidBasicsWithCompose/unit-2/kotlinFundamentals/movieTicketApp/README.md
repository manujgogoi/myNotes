# Movie Ticket App

```kotlin
fun main() {
    val child = 5
    val adult = 28
    val senior = 87

    val isMonday = true

    println("The movie ticket price for a person aged $child is \$${ticketPrice(child, isMonday)}.")
    println("The movie ticket price for a person aged $adult is \$${ticketPrice(adult, isMonday)}.")
    println("The movie ticket price for a person aged $senior is \$${ticketPrice(senior, isMonday)}.")
}

fun ticketPrice(age: Int, isMonday: Boolean): Int {
    val basePrice = when {
        age <= 12 -> 15
        age >= 65 -> 20
        else -> 25
    }

    // Apply discount on Mondays
    return if (isMonday) {
        (basePrice * 0.9).toInt()
    } else {
        basePrice
    }
}

```
