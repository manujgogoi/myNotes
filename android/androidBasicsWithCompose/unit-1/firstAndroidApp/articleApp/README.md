# Article App
```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            ComposeArticleTheme {
                // A surface container using the 'background' color from the theme
                Surface(
                    modifier = Modifier.fillMaxSize(),
                    color = MaterialTheme.colorScheme.background
                ) {
                    ArticleView(
                        title = stringResource(R.string.title),
                        paraOne = stringResource(R.string.para1),
                        paraTwo = stringResource(R.string.para2)
                    )
                }
            }
        }
    }
}

@Composable
fun ArticleView(title: String, paraOne: String, paraTwo: String,  modifier: Modifier = Modifier) {
    val image = painterResource(R.drawable.bg_compose_background)
    Column() {
        Image(
            painter = image,
            contentDescription = null,
        )
        Text(
            text = title,
            color = Color.Blue,
            fontSize = 30.sp,
            modifier = Modifier.fillMaxWidth()
                .padding(10.dp)
        )
        Text(
            text = paraOne,
            fontSize = 18.sp,
            textAlign = TextAlign.Justify,
            modifier = Modifier.fillMaxWidth()
                .padding(10.dp)
        )
        Text(
            text = paraTwo,
            fontSize = 18.sp,
            textAlign = TextAlign.Justify,
            modifier = Modifier.fillMaxWidth()
                .padding(10.dp)
        )
    }
}

@Preview(showBackground = true)
@Composable
fun GreetingPreview() {
    ComposeArticleTheme {
        ArticleView(
            title = stringResource(R.string.title),
            paraOne = stringResource(R.string.para1),
            paraTwo = stringResource(R.string.para2)
        )
    }
}
```