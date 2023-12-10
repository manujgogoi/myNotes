# States

- At its core, state in an app is any value that can change over time. This definition is very broad and includes everything from a database to a variable in your app.
- All Android apps display state to the user. A few examples of state in Android apps include:
  - A message that shows when a network connection can't be established.
  - Forms, such as registration forms. The state can be filled and submitted.
  - Tappable controls, such as buttons. The state could be **_not tapped_**, **_being tapped_** (display animation), or **_tapped_** (an action).

## Examples

```kotlin
import androidx.compose.runtime.MutableState
import androidx.compose.runtime.mutableStateOf

var amountInput: MutableState<String> = mutableStateOf("0")
```

The amountInput initialization can also be written like this with type inference:

```kotlin
var amountInput = mutableStateOf("0")
```

> Error: Creating a state object during composition without using remember.

In the TextField composable function, use the amountInput.value property:

```kotlin
TextField(
   value = amountInput.value,
   onValueChange = {},
   modifier = modifier
)
```

In the onValueChange named parameter's lambda expression, set the `amountInput.value` property to the `it` variable:

```kotlin
@Composable
fun EditNumberField(modifier: Modifier = Modifier) {
   var amountInput = mutableStateOf("0")
   TextField(
       value = amountInput.value,
       onValueChange = { amountInput.value = it },
       modifier = modifier
   )
}
```

## Use remember function to save state

Composable methods can be called many times because of recomposition. The composable resets its state during recomposition if it's not saved.

Composable functions can store an object across recompositions with the `remember`. A value computed by the `remember` function is stored in the Composition during initial composition and the stored value is returned during recomposition. Usually `remember` and `mutableStateOf` functions are used together in composable functions to have the state and its updates be reflected properly in the UI.

```kotlin
var amountInput by remember { mutableStateOf("") }
```

Use the remember function in EditNumberField() function:

1. In the `EditNumberField()` function, initialize the `amountInput` variable with the `by` `remember` Kotlin property `delegate`, by surrounding the call to `mutableStateOf()` function with `remember`.
2. In the `mutableStateOf()` function, pass in an empty string instead of a static `"0"` string:

```kotlin
var amountInput by remember { mutableStateOf("") }
```

Now the empty string is the initial default value for the `amountInput` variable. `by` is a **Kotlin property delegation**. The default getter and setter functions for the `amountInput` property are delegated to the `remember` class's getter and setter functions, respectively.

3. Import the following functions:

```kotlin
import androidx.compose.runtime.remember
import androidx.compose.runtime.getValue
import androidx.compose.runtime.setValue
```

Updated EditNumberField() function should look like this:

```kotlin
@Composable
fun EditNumberField(modifier: Modifier = Modifier) {
   var amountInput by remember { mutableStateOf("") }
   TextField(
       value = amountInput,
       onValueChange = { amountInput = it },
       modifier = modifier
   )
}
```

### Create an drawable xml file

1. Download the `svg` file (For example: from [pictogrammers.com](https://pictogrammers.com/library/mdi/))
2. In Android studio project select `app`
3. Right click on `app/res`
4. Then click on `new` > `Vector asset`
5. Asset Type = Local files
6. In Path: Select image (svg in my case)
7. Click on `Next` > `Finish`

The final code:

```kotlin
package com.example.tipcalculator

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.annotation.DrawableRes
import androidx.annotation.StringRes
import androidx.compose.foundation.layout.Arrangement
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Row
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.fillMaxWidth
import androidx.compose.foundation.layout.padding
import androidx.compose.foundation.layout.safeDrawingPadding
import androidx.compose.foundation.layout.size
import androidx.compose.foundation.layout.statusBarsPadding
import androidx.compose.foundation.layout.wrapContentWidth
import androidx.compose.foundation.rememberScrollState
import androidx.compose.foundation.text.KeyboardOptions
import androidx.compose.foundation.verticalScroll
import androidx.compose.material3.Icon
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.Surface
import androidx.compose.material3.Switch
import androidx.compose.material3.Text
import androidx.compose.material3.TextField
import androidx.compose.runtime.Composable
import androidx.compose.runtime.getValue
import androidx.compose.runtime.mutableStateOf
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.res.stringResource
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember
import androidx.compose.runtime.setValue
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.text.input.ImeAction
import androidx.compose.ui.text.input.KeyboardType
import androidx.compose.ui.text.style.TextAlign
import com.example.tipcalculator.ui.theme.TipCalculatorTheme
import java.text.NumberFormat

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            TipCalculatorTheme {
                // A surface container using the 'background' color from the theme
                Surface(
                    modifier = Modifier.fillMaxSize(),
                    color = MaterialTheme.colorScheme.background
                ) {
                    TipCalculatorApp()
                }
            }
        }
    }
}

@Composable
fun TipCalculatorApp(modifier: Modifier = Modifier) {
    var inputAmount by remember {mutableStateOf("")}
    var inputTip by remember { mutableStateOf("") }
    var roundUp by remember { mutableStateOf(false) }

    val amount = inputAmount.toDoubleOrNull() ?: 0.0
    val tipPercent = inputTip.toDoubleOrNull() ?: 0.0
    val tip = calculateTip(amount, tipPercent, roundUp)

    Column(
        modifier = modifier
            .fillMaxSize()
            .statusBarsPadding()
            .padding(horizontal = 20.dp)
            .verticalScroll(rememberScrollState())
            .safeDrawingPadding(),
        horizontalAlignment = Alignment.CenterHorizontally,
    ) {
        Column {
            Text(
                text = "Calculate Tip",
                modifier = modifier.padding(bottom = 16.dp, top = 40.dp),
            )
            EditNumberField(
                label = R.string.bill_amount,
                leadingIcon = R.drawable.cash_100,
                value = inputAmount,
                onValueChange = { inputAmount = it },
                modifier = modifier.padding(bottom = 32.dp),
                keyboardOptions = KeyboardOptions(
                    keyboardType = KeyboardType.Number,
                    imeAction = ImeAction.Next
                )
            )
            EditNumberField(
                label = R.string.how_was_the_service,
                leadingIcon = R.drawable.percent,
                value = inputTip,
                onValueChange = { inputTip = it },
                modifier = modifier.padding(bottom = 32.dp),
                keyboardOptions = KeyboardOptions(
                    keyboardType = KeyboardType.Number,
                    imeAction = ImeAction.Done
                )
            )
            RoundTheTipRow(
                roundUp = roundUp,
                onRoundUpChanged = { roundUp = it },
                modifier = Modifier.padding(bottom = 32.dp)
            )
            Text(
                text = stringResource(
                    R.string.tip_amount,
                    tip
                ),
                style = MaterialTheme.typography.headlineSmall,
                modifier = modifier
                    .padding(bottom = 30.dp)
                    .fillMaxWidth(),
                textAlign = TextAlign.Center
            )
        }
    }
}

@Composable
fun EditNumberField(
    @StringRes label: Int,
    @DrawableRes leadingIcon: Int,
    keyboardOptions: KeyboardOptions,
    value: String,
    onValueChange: (String) -> Unit,
    modifier: Modifier = Modifier
) {
    TextField(
        value = value,
        onValueChange = onValueChange,
        leadingIcon = { Icon(painter = painterResource(leadingIcon), contentDescription = "icon") },
        modifier = modifier
            .fillMaxWidth()
            .padding(bottom = 32.dp),
        label = { Text(stringResource(label)) },
        singleLine = true,
        keyboardOptions = keyboardOptions
    )
}

@Composable
fun RoundTheTipRow(
    roundUp: Boolean,
    onRoundUpChanged: (Boolean) -> Unit,
    modifier: Modifier = Modifier
) {
    Row(
        modifier = modifier
            .fillMaxWidth()
    ) {
        Text(text = stringResource(R.string.round_up_tip), modifier = modifier.padding(vertical = 10.dp))
        Switch(
            modifier = modifier
                .fillMaxWidth()
                .wrapContentWidth(Alignment.End)
                .padding(vertical = 0.dp),
            checked = roundUp,
            onCheckedChange = onRoundUpChanged
        )
    }
}

private fun calculateTip(
    amount: Double,
    tipPercent: Double = 15.0,
    roundUp: Boolean = false
): String {
    var tip = tipPercent / 100 * amount
    if (roundUp) {
        tip = kotlin.math.ceil(tip)
    }
    return NumberFormat.getCurrencyInstance().format(tip)
}

@Preview(showBackground = true, showSystemUi = true)
@Composable
fun GreetingPreview() {
    TipCalculatorTheme {
        TipCalculatorApp()
    }
}
```
