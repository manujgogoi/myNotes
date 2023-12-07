# Lamonade App (Typo: Lamonade)

```kotlin
package com.example.lamonade

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.Image
import androidx.compose.foundation.background
import androidx.compose.foundation.clickable
import androidx.compose.foundation.layout.Arrangement
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Row
import androidx.compose.foundation.layout.Spacer
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.fillMaxWidth
import androidx.compose.foundation.layout.height
import androidx.compose.foundation.layout.padding
import androidx.compose.foundation.shape.RoundedCornerShape
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.Surface
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.runtime.getValue
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember
import androidx.compose.runtime.setValue
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.res.stringResource
import androidx.compose.ui.text.font.FontFamily
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.text.style.TextAlign
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import com.example.lamonade.ui.theme.LamonadeTheme

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            LamonadeTheme {
                // A surface container using the 'background' color from the theme
                Surface(
                    modifier = Modifier.fillMaxSize(),
                    color = MaterialTheme.colorScheme.background
                ) {
                    LemonadeAppScreen(modifier = Modifier)
                }
            }
        }
    }
}

@Composable
fun MyScreen(onClick: (Int) -> Unit, screen: Int, modifier: Modifier) {
    val image = when(screen) {
        1 -> painterResource(R.drawable.lemon_tree)
        2 -> painterResource(R.drawable.lemon_squeeze)
        3 -> painterResource(R.drawable.lemon_drink)
        4 -> painterResource(R.drawable.lemon_restart)
        else -> painterResource(R.drawable.lemon_tree)
    }

    val instruction = when(screen) {
        1 -> stringResource(R.string.tap_lemon_tree_to_select_a_lemon)
        2 -> stringResource(R.string.keep_tapping_the_lemon)
        3 -> stringResource(R.string.tap_the_lemonade)
        4 -> stringResource(R.string.tap_the_empty_glass)
        else -> stringResource(R.string.tap_lemon_tree_to_select_a_lemon)
    }

    val description = when(screen) {
        1 -> stringResource(R.string.lemon_tree)
        2 -> stringResource(R.string.lemon)
        3 -> stringResource(R.string.glass_of_lemonade)
        4 -> stringResource(R.string.empty_glass)
        else -> stringResource(R.string.lemon_tree)
    }
    Column(
        modifier = modifier.fillMaxSize(),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Row(
            modifier.background(color = Color(0xFFD6E7E9), shape = RoundedCornerShape(20.dp))
        ) {
            Image(
                painter = image,
                contentDescription = description,
                modifier.clickable { onClick(screen) }.padding(30.dp)
            )
        }
        Spacer(modifier = Modifier.height(40.dp))
        Text(
            text = instruction,
            fontSize = 20.sp,
            fontFamily = FontFamily.SansSerif,
            fontWeight = FontWeight(400)
        )
    }
}

@Composable
fun LemonadeAppScreen(modifier: Modifier = Modifier) {
    var screen by remember { mutableStateOf(1) }
    var attempt = (2..4).random()
    val imageClicked: (currentScreen: Int) -> Unit = {
        attempt--
        when(it) {
            1 -> screen = 2
            2 -> screen = if(attempt > 0) 2 else 3
            3 -> screen = 4
            else -> screen = 1
        }
    }
    Column(
        modifier = modifier.fillMaxSize()
    ) {
        Column(
            modifier = modifier
                .fillMaxWidth()
                .background(Color(0xFFFFEB3B))
                .padding(10.dp)
        ) {
            Text(
                text = stringResource(R.string.app_name),
                modifier = modifier.fillMaxWidth(),
                textAlign = TextAlign.Center,
                fontSize = 25.sp,
                fontWeight = FontWeight.Bold
            )
        }
        MyScreen(imageClicked, screen, modifier = modifier)
    }
}

@Preview(showBackground = true)
@Composable
fun LemonadeApp(modifier: Modifier = Modifier) {
    LemonadeAppScreen(modifier = modifier)
}
```
