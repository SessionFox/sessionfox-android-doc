SessionFox library for Android can be integrated in Android applications. The library is supported from API Level: 16, Android 4.1 (JELLY BEAN)
SessionFox SDK should be triggered at the beginning of application launch.

### Including library in Android project

1. Create a new project in Android Studio or Open an existing application project

2. In the app build.gradle, add following inside allprojects.repositories

```
allprojects{
    repositories {
        google()
        jcenter()
        maven {
            url "https://mymavenrepo.com/repo/PENxspKoeuoFCKp9veSD/"
        }  
    }
}
```

3. In the app build.gradle, add following snippet inside dependencies
```java
implementation ('com.sessionfox:sessionfox-sdk:1.0.8-alpha@aar') {
  transitive = true
  }
```
    
4. In your Android Manifest, add the following line
```xml <meta-data android:name="SESSION_FOX_API_KEY" android:value="<your-api-key>" />```

Please replace  with app token obtained from support@sessionfox.com.

5. Extend Application class(if not already extended) and add this line to your onCreate()
```java
SessionFox.init(this);

// Tag screen name visited
SessionFox.setScreen("com.sample.CheckoutScreen");

// Send custom user meta data
SessionFox.setUser(userHashmap);

// Send custom event
SessionFox.sendEvent("purchase",purchaseDetailsHashmap);
```
