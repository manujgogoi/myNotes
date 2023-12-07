# Foldable Phones

## Version 1

```kotlin
open class Phone(var isScreenLightOn: Boolean = false){
    open fun switchOn() {
        isScreenLightOn = true
    }

    fun switchOff() {
        isScreenLightOn = false
    }

    fun checkPhoneScreenLight() {
        val phoneScreenLight = if (isScreenLightOn) "on" else "off"
        println("The phone screen's light is $phoneScreenLight.")
    }
}

class FoldablePhone(isScreenLightOn: Boolean = false, var isFolded: Boolean = false) : Phone(isScreenLightOn) {
    override fun switchOn() {
        if(isFolded) {
            isScreenLightOn = false
        } else {
            isScreenLightOn = true
        }
    }

    fun fold() {
        isFolded = true;
        switchOff()
    }

    fun unFold() {
        isFolded = false
    }
}

fun main() {
    val myPhone = Phone()
    myPhone.checkPhoneScreenLight()
    myPhone.switchOn()
    myPhone.checkPhoneScreenLight()
    myPhone.switchOff()
    myPhone.checkPhoneScreenLight()
    println("-------------------")
    val myFoldablePhone = FoldablePhone()
    myFoldablePhone.checkPhoneScreenLight()
    myFoldablePhone.switchOn()
    myFoldablePhone.checkPhoneScreenLight()
    myFoldablePhone.fold()
    myFoldablePhone.checkPhoneScreenLight()
}
```

Output:

```bash
The phone screen's light is off.
The phone screen's light is on.
The phone screen's light is off.
-------------------
The phone screen's light is off.
The phone screen's light is on.
The phone screen's light is off.
```
