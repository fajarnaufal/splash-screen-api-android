# Android 12 Splash Screen API Implementation

A simple Android project demonstrating the implementation of Android 12 Splash Screen API using Animated Vector Drawable (AVD).

## 📱 Overview

This project showcases how to implement the modern Splash Screen API introduced in Android 12, which provides a standardized and simplified way to create splash screens without the need for custom implementations.

## ✨ Features

- Android 12+ Splash Screen API implementation
- Animated Vector Drawable (AVD) support
- Clean and simple setup
- Modern Kotlin DSL with Gradle version catalogs

## 🛠️ Technologies Used

- **Language**: Kotlin
- **Build System**: Gradle (Kotlin DSL)
- **Min SDK**: Android 12 (API 31)
- **Dependencies**:
  - AndroidX Core Splash Screen Library (`androidx.core:core-splashscreen:1.2.0`)

## 📋 Setup Instructions

### 1. Add Dependency

In your `build.gradle.kts (app)`:

```kotlin
implementation(libs.androidx.core.splashscreen)
```

In your `libs.versions.toml`:

```toml
[versions]
coreSplashscreen = "1.2.0"

[libraries]
androidx-core-splashscreen = { module = "androidx.core:core-splashscreen", version.ref = "coreSplashscreen" }
```

### 2. Add Animated Vector Drawable

Add your AVD XML file to the `res/drawable` folder. You can use the example from the [Android documentation](https://developer.android.com/develop/ui/views/launch/splash-screen).

```xml
<animated-vector xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:aapt="http://schemas.android.com/aapt">
    <aapt:attr name="android:drawable">
        <vector
            android:width="432dp"
            android:height="432dp"
            android:viewportWidth="432"
            android:viewportHeight="432">
            <group android:name="_R_G">
                <!-- Your vector path here -->
            </group>
        </vector>
    </aapt:attr>
</animated-vector>
```

### 3. Create Splash Screen Theme

In your `res/values/themes.xml`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <!--Splash Screen Theme-->
    <style name="Theme.App.Starting" parent="Theme.SplashScreen">
        <item name="windowSplashScreenBackground">@color/white</item>
        <item name="windowSplashScreenAnimatedIcon">@drawable/example_google</item>
        <item name="windowSplashScreenAnimationDuration">1000</item>
        <item name="postSplashScreenTheme">@style/Theme.SplashScreenAPI</item>
    </style>

    <!--App Theme-->
    <style name="Theme.SplashScreenAPI" parent="android:Theme.Material.Light.NoActionBar" />
</resources>
```

### 4. Update AndroidManifest.xml

Set the splash screen theme to your launcher activity:

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android">
    <application
        android:theme="@style/Theme.SplashScreenAPI"
        ...>
        <activity
            android:name=".MainActivity"
            android:exported="true"
            android:theme="@style/Theme.App.Starting">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>
```

### 5. Initialize in MainActivity

Call `installSplashScreen()` before `super.onCreate()`:

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        val splashScreen = installSplashScreen()
        super.onCreate(savedInstanceState)

        enableEdgeToEdge()
        setContent {
            // Your Compose content here
        }
    }
}
```

## 🎨 Theme Attributes Explanation

| Attribute | Description |
|-----------|-------------|
| `windowSplashScreenBackground` | Sets the background color of the splash screen |
| `windowSplashScreenAnimatedIcon` | Sets the icon/animation displayed in the center |
| `windowSplashScreenAnimationDuration` | Duration of the icon animation (for Android 12 only) |
| `postSplashScreenTheme` | The theme to use after the splash screen is dismissed |

## 📝 Notes

- For Android 13+, the animation duration is automatically inferred from the `AnimatedVectorDrawable`
- The `windowSplashScreenAnimationDuration` doesn't affect the actual splash screen display time, only the icon animation
- Always call `installSplashScreen()` before `super.onCreate()`

## 🔗 Resources

- [Official Android Splash Screen Documentation](https://developer.android.com/develop/ui/views/launch/splash-screen)
- [Medium Article](https://medium.com/@naufalfajarimani/implementing-android-12-splash-screen-api-with-animated-vector-drawable-avd-2f52fe54b63f) - Detailed tutorial

## 📄 License

This project is available under the MIT License.

## 🤝 Contributing

Feel free to open issues or submit pull requests if you find any bugs or have suggestions for improvements.

---

Made with ❤️ by Naufal Fajar Imani and Github Copilot
