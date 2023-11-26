# CheatSheet

## Image

```kotlin
import androidx.compose.foundation.Image
...
...
...

val image = painterResource(R.drawable.android_logo)
Image(
    painter = image,
    contentDescription = null,
    Modifier
        .size(150.dp)
        .background(Color(0xFF0F3C4E))
)
```

## Icons

```kotlin
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.Person
import androidx.compose.material3.Icon
...
...
...
Icon(
    modifier = Modifier
        .size(size = 120.dp)
        .background(color = Color.LightGray),
    imageVector = Icons.Default.Person,
    contentDescription = "Person Icon"
)
```

## when condition

```kotlin
fun main() {
    val x: Any = 20

    when (x) {
        2, 3, 5, 7 -> println("x is a prime number between 1 and 10.")
        in 1..10 -> println("x is a number between 1 and 10, but not a prime number.")
        is Int -> println("x is an integer number, but not between 1 and 10.")
        else -> println("x isn't an integer number.")
    }
}
```

## if condition

```kotlin
fun main() {
    val trafficLightColor = "Black"

    val message =
      if (trafficLightColor == "Red") "Stop"
      else if (trafficLightColor == "Yellow") "Slow"
      else if (trafficLightColor == "Green") "Go"
      else "Invalid traffic-light color"

    println(message)
}
```

## Nullable

In Kotlin, there's a distinction between nullable and non-nullable types:

- Nullable types are variables that can hold `null`.
- Non-null types are variables that can't hold `null`.

To declare nullable variables in Kotlin, you need to add a `?` operator to the end of the type.
