# Generics

## Codes

### Version 1

```kotlin
fun main() {

    Quiz.printProgressBar()

}

// Enum
enum class Difficulty{
    EASY, MEDIUM, HARD
}

class Quiz {
    val question1 = Question<String>("Quoth the Raven ___", "nevermore", Difficulty.MEDIUM)
    val question2 = Question<Boolean>("The sky is green. True or false", false, Difficulty.EASY)
    val question3 = Question<Int>("How many days are there between full moons?", 28, Difficulty.HARD)

    // Companion Singleton Object
    companion object StudentProgress {
        val total: Int = 10
        val answered: Int = 3
    }
}

// Add an extension property
val Quiz.StudentProgress.progressText: String
	get() = "${answered} of ${total} answered"

// Add an extension function
fun Quiz.StudentProgress.printProgressBar() {
    repeat(Quiz.answered) {print("▓")}
    repeat(Quiz.total - Quiz.answered) {print("▒")}
    println()
    println(Quiz.progressText)
}

// Data class: Because, they don't have any methods that perform an action.
data class Question<T>(
	val questionText: String,
    val answer: T,
    val difficulty: Difficulty
)
```

### Version 2 (Using Interface)

```kotlin
fun main() {

    Quiz().printProgressBar()

}

// Enum
enum class Difficulty{
    EASY, MEDIUM, HARD
}

// Interface
interface ProgressPrintable {
    val progressText: String
    fun printProgressBar()
}

class Quiz : ProgressPrintable {
    val question1 = Question<String>("Quoth the Raven ___", "nevermore", Difficulty.MEDIUM)
    val question2 = Question<Boolean>("The sky is green. True or false", false, Difficulty.EASY)
    val question3 = Question<Int>("How many days are there between full moons?", 28, Difficulty.HARD)

    override val progressText: String
    	get() = "${answered} of ${total} answered"

    override fun printProgressBar() {
        repeat(Quiz.answered) {print("▓")}
        repeat(Quiz.total - Quiz.answered) {print("▒")}
        println()
        println(progressText)
    }

    // Companion Singleton Object
    companion object StudentProgress {
        val total: Int = 10
        val answered: Int = 3
    }
}

// Data class: Because, they don't have any methods that perform an action.
data class Question<T>(
	val questionText: String,
    val answer: T,
    val difficulty: Difficulty
)
```

### Use of Scope functions : let() and apply()

```kotlin
fun main() {

    //Quiz().printProgressBar()

    //var quiz = Quiz()
    //quiz.printQuiz()

    val quiz = Quiz().apply {
        printQuiz()
        printProgressBar()
    }

}

// Enum
enum class Difficulty{
    EASY, MEDIUM, HARD
}

// Interface
interface ProgressPrintable {
    val progressText: String
    fun printProgressBar()
}

class Quiz : ProgressPrintable {
    val question1 = Question<String>("Quoth the Raven ___", "nevermore", Difficulty.MEDIUM)
    val question2 = Question<Boolean>("The sky is green. True or false", false, Difficulty.EASY)
    val question3 = Question<Int>("How many days are there between full moons?", 28, Difficulty.HARD)

    override val progressText: String
    	get() = "${answered} of ${total} answered"

    override fun printProgressBar() {
        repeat(Quiz.answered) {print("▓")}
        repeat(Quiz.total - Quiz.answered) {print("▒")}
        println()
        println(progressText)
    }

    // Companion Singleton Object
    companion object StudentProgress {
        val total: Int = 10
        val answered: Int = 3
    }

    // Print method
    fun printQuiz() {
        question1.let {
            println(it.questionText)
            println(it.answer)
            println(it.difficulty)
        }
        println()

        question2.let {
            println(it.questionText)
            println(it.answer)
            println(it.difficulty)
        }
        println()

        question3.let {
            println(it.questionText)
            println(it.answer)
            println(it.difficulty)
        }
        println()
    }
}

// Data class: Because, they don't have any methods that perform an action.
data class Question<T>(
	val questionText: String,
    val answer: T,
    val difficulty: Difficulty
)
```
