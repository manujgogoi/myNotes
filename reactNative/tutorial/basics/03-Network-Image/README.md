# Network Image with `SafeAreaView` and `ScrollView`

```tsx
import React from "react";
import { Image, SafeAreaView, ScrollView, Text, View } from "react-native";

const App = () => {
  return (
    <SafeAreaView>
      <ScrollView style={{ paddingHorizontal: 5, backgroundColor: "#223399" }}>
        <Text>Hello Kitty</Text>
        <View>
          <Text style={{ color: "#ffff" }}>Image of a cat</Text>
          <Image
            source={{ uri: "https://reactnative.dev/docs/assets/p_cat2.png" }}
            style={{ width: 200, height: 200 }}
          />
        </View>
      </ScrollView>
    </SafeAreaView>
  );
};

export default App;
```
