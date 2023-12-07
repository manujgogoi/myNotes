# Internet Profile

## Version 1

```kotlin
fun main() {
    val amanda = Person("Amanda", 33, "play tennis", null)
    val atiqah = Person("Atiqah", 28, "climb", amanda)

    amanda.showProfile()
    atiqah.showProfile()
}


class Person(val name: String, val age: Int, val hobby: String?, val referrer: Person?) {
    fun showProfile() {
       println("Name: ${name}")
       println("Age: ${age}")
       if(referrer != null) {
           println("Likes to ${hobby ?: "do nothing"}. Has a referrer named ${referrer.name}, who likes to ${referrer.hobby ?: "do nothing"}.")
       } else {
           println("Likes to ${hobby ?: "do nothing"}. Doesn't have a referrer.")
       }
    }
}
```

## Version 2

```kotlin
fun main() {
    val amanda = Person("Amanda", 33, "play tennis", null)
    val atiqah = Person("Atiqah", 28, "climb", amanda)

    amanda.showProfile()
    atiqah.showProfile()
}

class Person(val name: String, val age: Int, val hobby: String?, val referrer: Person?) {
    fun showProfile() {
        println("Name: $name")
        println("Age: $age")
        println("Likes to ${hobby ?: "do nothing"}. ${getReferrerInfo()}")
    }

    private fun getReferrerInfo(): String {
        return if (referrer != null) {
            "Has a referrer named ${referrer.name}, who likes to ${referrer.hobby ?: "do nothing"}."
        } else {
            "Doesn't have a referrer."
        }
    }
}

```
