# Song Catalog

## Version 1

```kotlin
class Song(val title: String, val artist: String, val yearPublished: Int, val playCount: Int) {
    val isPopular: Boolean
        get() {
            return if(playCount < 1000) false else true
        }
    fun songDescription() {
        println("$title, performed by $artist, was released in $yearPublished.")
    }
}

fun main() {
    val mySong = Song(title="My Song", artist="Sonu Nigam", yearPublished=2023, playCount=100)
    mySong.songDescription()
    println("${if(mySong.isPopular) "Popular" else "Not popular"}")
}
```

## Version 2

```kotlin
class Song(val title: String, val artist: String, val yearPublished: Int, val playCount: Int) {
    	val isPopular: Boolean
    		get() = playCount >= 1000

        fun printDescription() {
            println("\"$title\", performed by $artist, was released in $yearPublished.")
        }
}

fun main() {
    val song1 = Song("Song Title 1", "Artist 1", 2020, 1200)
    val song2 = Song("Song Title 2", "Artist 2", 2022, 800)

    song1.printDescription()
    println("Is song1 popular? ${song1.isPopular}")

    song2.printDescription()
    println("Is song2 popular? ${song2.isPopular}")
}
```
