# Loading Network images on MacOS (Error)

Solution:

Add the following code to the `DebugProfile.entitlements` file under `macos/Runner/` directory

```html
<key>com.apple.security.network.client</key> <true />
```
