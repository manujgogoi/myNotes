# Automated Testing

> I'm using the `tipCalculator` app for testing which was created in `StatesInCompose` section

## Type of automated tests

### Local tests

- Local tests are a type of automated test that directly test a small piece of code to ensure that it functions properly.
- With local tests, you can test functions, classes, and properties.
- Local tests are executed on your workstation, which means they run in a development environment without the need for a device or emulator.
- Android Studio comes ready to run local tests automatically.

### Instrumentation tests

- For Android development, an instrumentation test is a UI test.
- Instrumentation tests let you test parts of an app that depend on the Android API, and its platform APIs and services.

## Local tests (tipCalculator App)

- change visibility of `calculateTip()` method from `private` to `internal`

- Add the `@VisibleForTesting` annotation:

```kotlin
@VisibleForTesting
internal fun calculateTip(amount: Double, tipPercent: Double = 15.0, roundUp: Boolean): String {
    var tip = tipPercent / 100 * amount
    if (roundUp) {
        tip = kotlin.math.ceil(tip)
    }
    return NumberFormat.getCurrencyInstance().format(tip)
}
```

### Create test directory

- In the `Project` tab, change the view to `Project`
- In the `Project` view click `src` > `New` > `Directory` > Select the `test/Java` (create if not exists)
- Right click on `Java` > `New` > `Package` > Name it `com.example.tipCalculator`
- Right click on `com.example.tipCalculator` package > `New` > `Kotlin Class/File` > Give a name: `TipCalculatorTest` > then select `Class`

### Write the test cases

```kotlin
package com.example.tipcalculator

import org.junit.Assert.assertEquals
import org.junit.Test
import java.text.NumberFormat

class TipCalculatorTest {

    @Test
    fun calculateTip_20PercentNoRoundUp() {
        val amount = 10.00;
        val tipPercent = 20.00;
        val expectedTip = NumberFormat.getCurrencyInstance().format(2);
        val actualTip = calculateTip(amount = amount, tipPercent = tipPercent, false);
        assertEquals(expectedTip, actualTip);
    }
}
```

- You may have noticed that arrows appear in the gutter alongside the line number of your class name and test function. You can click these arrows to run the test.

## Instrumentation tests

### Create the instrumentation directory

- In `Project` view right click on `app/src` > `New` > `Directory`
- In `New Directory` select `androidTest/java`
- Right click on the `androidTest/java` folder and select `New` > `Package`.
- In the `New Package` window, type `com.example.tipCalculator`

### Create a test case

- In Android projects, the instrumentation test directory is designated as the `androidTest` directory.
- Right click on `com.example.tipcalculator` package > `New` > `Kotlin Class/File`
- In `New Kotlin Class/File` window type the class name: `TipUITests` and select `class`.
- In `TipUITests` class file add the following code and run the test.

```kotlin
package com.example.tipcalculator

import androidx.compose.ui.test.junit4.createComposeRule
import androidx.compose.ui.test.onNodeWithText
import androidx.compose.ui.test.performTextInput
import com.example.tipcalculator.ui.theme.TipCalculatorTheme
import org.junit.Rule
import org.junit.Test
import java.text.NumberFormat

class TipUITests {
    @get:Rule
    val composeTestRule = createComposeRule()

    @Test
    fun calculate_20_percent_tip() {
        composeTestRule.setContent {
            TipCalculatorTheme {
                TipCalculatorApp()
            }
        }

        composeTestRule.onNodeWithText("Bill Amount")
            .performTextInput("10")

        composeTestRule.onNodeWithText("Tip Percentage")
            .performTextInput("20")

        val expectedTip = NumberFormat.getCurrencyInstance().format(2)
        composeTestRule.onNodeWithText("Tip Amount: $expectedTip")
            .assertExists("No Node with this text was found")
    }
}
```
