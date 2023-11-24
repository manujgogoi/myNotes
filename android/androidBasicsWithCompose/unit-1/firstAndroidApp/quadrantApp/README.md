# Quadrant App

## Layout Basics (Column and Rows)

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            QuadrantTheme {
                // A surface container using the 'background' color from the theme
                Surface(
                    modifier = Modifier.fillMaxSize(),
                    color = MaterialTheme.colorScheme.background
                ) {
                    Quadrant()
                }
            }
        }
    }
}

@Composable
fun Card(title: String, body: String, backgroundColor: Color, modifier: Modifier = Modifier) {
    Column(
        modifier = modifier
            .fillMaxSize()
            .background(backgroundColor)
            .padding(16.dp),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Text(
            text = title,
            modifier = Modifier.padding(bottom = 10.dp),
            fontWeight = FontWeight.Bold
        )
        Text(
            text = body,
            textAlign = TextAlign.Justify
        )
    }
}

@Composable
fun Quadrant(modifier: Modifier = Modifier) {
    Column(
        modifier = modifier.fillMaxSize()
    ) {
        Row(
            Modifier.weight(1f)
        ) {
            Card(
                title = stringResource(R.string.text_composable),
                body = stringResource(R.string.text_composable_body),
                backgroundColor = Color(0xFFEADDFF),
                modifier = Modifier.weight(1f))
            Card(
                title = stringResource(R.string.image_composable),
                body = stringResource(R.string.image_composable_body),
                backgroundColor = Color(0xFFD0BCFF),
                modifier = Modifier.weight(1f))
        }
        Row(
            Modifier.weight(1f)
        ) {
            Card(
                title = stringResource(R.string.row_composable),
                body = stringResource(R.string.row_composable_body),
                backgroundColor = Color(0xFFB69DF8),
                modifier = Modifier.weight(1f))
            Card(
                title = stringResource(R.string.column_composable),
                body = stringResource(R.string.column_composable_body),
                backgroundColor = Color(0xFFF6EDFF),
                modifier = Modifier.weight(1f))
        }
    }
}

@Preview(showBackground = true)
@Composable
fun GreetingPreview() {
    QuadrantTheme {
        Quadrant()
    }
}
```
