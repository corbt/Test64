This React Native project demonstrates crashing behavior on a Nexus 9 (and presumably other 64bit ARM devices).

The only difference between it and a vanilla React Native project is that I've added `compile 'io.realm:realm-android:0.82.2'` to the `android/app/build.gradle` file.

The reason it fails is likely due to the fact that Android can't mix 32 and 64bit native libraries, and `realm-android` contains a 64bit native library.

Run on a Nexus 9, the stacktrace is as follows:

```
E/AndroidRuntime(15519): FATAL EXCEPTION: main
E/AndroidRuntime(15519): Process: com.test64, PID: 15519
E/AndroidRuntime(15519): java.lang.UnsatisfiedLinkError: could find DSO to load: libreactnativejni.so
E/AndroidRuntime(15519):  at com.facebook.soloader.SoLoader.loadLibraryBySoName(SoLoader.java:213)
E/AndroidRuntime(15519):  at com.facebook.soloader.SoLoader.loadLibrary(SoLoader.java:178)
E/AndroidRuntime(15519):  at com.facebook.react.bridge.JSCJavaScriptExecutor.<clinit>(JSCJavaScriptExecutor.java:19)
E/AndroidRuntime(15519):  at com.facebook.react.ReactInstanceManager.onJSBundleLoadedFromServer(ReactInstanceManager.java:310)
E/AndroidRuntime(15519):  at com.facebook.react.ReactInstanceManager.access$100(ReactInstanceManager.java:70)
E/AndroidRuntime(15519):  at com.facebook.react.ReactInstanceManager$1.onJSBundleLoadedFromServer(ReactInstanceManager.java:97)
E/AndroidRuntime(15519):  at com.facebook.react.devsupport.DevSupportManager$13$1.run(DevSupportManager.java:530)
E/AndroidRuntime(15519):  at android.os.Handler.handleCallback(Handler.java:739)
E/AndroidRuntime(15519):  at android.os.Handler.dispatchMessage(Handler.java:95)
E/AndroidRuntime(15519):  at android.os.Looper.loop(Looper.java:135)
E/AndroidRuntime(15519):  at android.app.ActivityThread.main(ActivityThread.java:5254)
E/AndroidRuntime(15519):  at java.lang.reflect.Method.invoke(Native Method)
E/AndroidRuntime(15519):  at java.lang.reflect.Method.invoke(Method.java:372)
E/AndroidRuntime(15519):  at com.android.internal.os.ZygoteInit$MethodAndArgsCaller.run(ZygoteInit.java:903)
E/AndroidRuntime(15519):  at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:698)
```