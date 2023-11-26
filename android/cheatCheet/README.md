# CheatSheet

## Image

```kotlin
import androidx.compose.foundation.Image
...
...
...

val image = painterResource(R.drawable.android_logo)
Image(
    painter = image,
    contentDescription = null,
    Modifier
        .size(150.dp)
        .background(Color(0xFF0F3C4E))
)
```

## Icons

```kotlin
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.Person
import androidx.compose.material3.Icon
...
...
...
Icon(
    modifier = Modifier
        .size(size = 120.dp)
        .background(color = Color.LightGray),
    imageVector = Icons.Default.Person,
    contentDescription = "Person Icon"
)
```
