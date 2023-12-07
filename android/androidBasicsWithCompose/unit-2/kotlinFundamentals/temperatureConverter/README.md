# Temperature Converter App

```kotlin
fun main() {
    printFinalTemperature(27.0, "Celsius", "Fahrenheit") { celsiusToFahrenheit(it) }
    printFinalTemperature(350.0, "Kelvin", "Celsius") { kelvinToCelsius(it) }
    printFinalTemperature(10.0, "Fahrenheit", "Kelvin") { fahrenheitToKelvin(it) }
}

fun celsiusToFahrenheit(celsius: Double): Double {
    return celsius * 9 / 5 + 32
}

fun kelvinToCelsius(kelvin: Double): Double {
    return kelvin - 273.15
}

fun fahrenheitToKelvin(fahrenheit: Double): Double {
    return (fahrenheit - 32) * 5 / 9 + 273.15
}


fun printFinalTemperature(
    initialMeasurement: Double,
    initialUnit: String,
    finalUnit: String,
    conversionFormula: (Double) -> Double
) {
    val finalMeasurement = String.format("%.2f", conversionFormula(initialMeasurement)) // two decimal places
    println("$initialMeasurement degrees $initialUnit is $finalMeasurement degrees $finalUnit.")
}
```
