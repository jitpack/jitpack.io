# Android library builds

Android SDK is available in the build environment and ANDROID_HOME variable is already set when the build starts.

## Gradle

To enable installing into local maven repository and JitPack you need to add the 'android-maven' plugin:

 1. Add `classpath 'com.github.dcendents:android-maven-plugin:1.2'` to root build.gradle under `buildscripts`
 2. Add `apply plugin: 'android-maven'` to the library/build.gradle

After these changes you should be able to run:

    gradle install
    
That's it. If install works and you have added a GitHub release it should work jitpack.io

## Examples

- Android-Example https://github.com/jitpack/android-example

## Installing

Users of your library will need add the jitpack.io repository:

```gradle
repositories {
    maven {
      url "https://jitpack.io"
    }
}
```

and:

```gradle
dependencies {
    compile 'com.github.jitpack:android-example:1.0.1'
}
```

## Other notes

- Android NDK builds are not yet supported on JitPack

