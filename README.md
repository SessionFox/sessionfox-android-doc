SessionFox library for Android can be integrated in Android applications. The library is supported from API Level: 16, Android 4.1 (JELLY BEAN)
SessionFox SDK should be triggered at the beginning of application launch.

### Including library in Android project

#### Step 1
In the app build.gradle, add following inside allprojects.repositories

```
allprojects{
    repositories {
        google()
        jcenter()
        maven {
            url "https://mymavenrepo.com/repo/EpCerWf2f0TbbXSSpgLb/"
        }  
    }
}
```

and the following snippet inside dependencies
```java
implementation ('com.sessionfox:sessionfox-sdk:1.1.4-alpha@aar') {
  transitive = true
}
```
The SDK needs compatibility with java 1.8, so please make sure the bellow lines are added
```java
android {
    compileOptions {
        targetCompatibility 1.8
        sourceCompatibility 1.8
    }
}
```
#### Step 2
In your Android Manifest, add the following line

```xml
<meta-data android:name="SESSION_FOX_API_KEY" android:value="<your-api-key>" />
```

Please replace  with app token obtained from sankalp@sessionfox.com.

#### Step 3
Extend Application class(if not already extended) and add this line to your `onCreate()`
```java
SessionFox.init(this);
```

Thats it! you are now ready to use sessionfox

### Usage
Available APIs
```java
// Tag screen name visited
SessionFox.setScreen("com.sample.CheckoutScreen");

// Send custom event
SessionFox.sendEvent("purchase",purchaseDetailsHashmap);

// To report an issue with ui
SessionFox.showDialog(context);

// To report an issue with own ui
SessionFox.reportIssue(<report message>, <meta data hashmap>);
```
### Using Proguard with the SessionFox SDK
If your app is proguarded, you may notice some errors at the time of making a release apk. If this happens, add the following lines to the end of your proguard-rules.pro
```
# Class names are needed in reflection
-keepnames class com.amazonaws.**
-keepnames class com.amazon.**
# Request handlers defined in request.handlers
-keep class com.amazonaws.services.**.*Handler
# The following are referenced but aren't required to run
-dontwarn com.fasterxml.jackson.**
-dontwarn org.apache.commons.logging.**
# Android 6.0 release removes support for the Apache HTTP client
-dontwarn org.apache.http.**
# The SDK has several references of Apache HTTP client
-dontwarn com.amazonaws.http.**
-dontwarn com.amazonaws.metrics.**
```
