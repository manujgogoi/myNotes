# Classes and Collections

## Example code

```kotlin
fun main() {
    val event1 = Event(
        title = "Wake Up",
        description = "Time to wake up!",
        daypart = DayPart.MORNING,
        durationInMinutes = 0
    )

    val event2 = Event(
        title = "Eat breakfast",
        daypart = DayPart.MORNING,
        durationInMinutes = 15
    )

    val event3 = Event(
        title = "Learn about Kotlin",
        daypart = DayPart.AFTERNOON,
        durationInMinutes = 30
    )

    val event4 = Event(
        title = "Practice Compose",
        daypart = DayPart.AFTERNOON,
        durationInMinutes = 60
    )

     val event5 = Event(
        title = "Watch latest DevBytes video",
        daypart = DayPart.AFTERNOON,
        durationInMinutes = 10
    )

     val event6 = Event(
        title = "Check out latest Android Jetpack library",
        daypart = DayPart.EVENING,
        durationInMinutes = 45
    )

    // All events
    val events = mutableListOf<Event>(event1, event2, event3, event4, event5, event6)

    // Short events
    val shortEvents = events.filter { it.durationInMinutes < 60 }
    println("You have ${shortEvents.size} short events.")

    // Grouped events
    val groupedEvents = events.groupBy { it.daypart }

    groupedEvents.forEach{ (daypart, events) ->
        println("${daypart}: ${events.size} events")

    }

    // Last item
    println("Last event of the day: ${events.last().title}")

    // Event duration using extension property
    println("Duration of first event of the day: ${events[0].durationOfEvent}")
}

enum class DayPart {
    MORNING,
    AFTERNOON,
    EVENING
}

data class Event(
	val title: String,
    val description: String? = null,
    val daypart: DayPart,
    val durationInMinutes: Int
)

val Event.durationOfEvent: String
	get() = if (this.durationInMinutes < 60) {
        "short"
    } else {
        "long"
    }



```
