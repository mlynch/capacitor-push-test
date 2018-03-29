First, we need to add the Google Services references to our app:

Add to your root `build.gradle`:

```gradle
buildscript {
  // ...
    dependencies {
        classpath 'com.android.tools.build:gradle:3.0.1'
        // Add this line:
        classpath 'com.google.gms:google-services:3.2.0'
    }
}

// Add this block
allprojects {
    repositories {
        google()
        jcenter()
        maven {
            url "https://maven.google.com" // Google's Maven repository
        }
    }
}
}
```

Next, we need to add the dependencies for Ionic Push Notifications as well as Firebase. This is required because
Capacitor's push notifications uses FCM which must be referenced in your app's gradle to function properly.

Add to your `app/build.gradle`:

```gradle
dependencies {
  // ... other dependecies above here
  implementation 'ionic-team:ionic-native-plugins-core:0.0.4'
  implementation 'ionic-team:ionic-native-push-notifications:0.0.4'
  compile 'com.google.firebase:firebase-core:12.0.1'
  compile 'com.google.android.gms:play-services-base:12.0.1'
  compile 'com.google.android.gms:play-services-location:12.0.1'
}

apply from: 'capacitor.build.gradle'
apply plugin: 'com.google.gms.google-services'
```

Next, there are two services that need to be linked in your Android Manifest:

Add to your `AndroidManifest.xml`:

<service
    android:name="com.ionicframework.nativeplugins.push.PushNotificationsInstanceIdService">
    <intent-filter>
        <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
    </intent-filter>
</service>
<service
    android:name="com.ionicframework.nativeplugins.push.PushNotificationsMessagingService">
    <intent-filter>
        <action android:name="com.google.firebase.MESSAGING_EVENT"/>
    </intent-filter>
</service>

Install `capacitor-push-notifications`:

```bash
npm install capacitor-push-notifications
```

Update platforms:

```bash
npx cap update
```
