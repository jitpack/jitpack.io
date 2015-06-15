# Android library builds

Android SDK is available in the build environment and ANDROID_HOME variable is already set when the build starts.
Builds are run with Java 7 by default.

## Gradle

To enable installing into local maven repository and JitPack you need to add the [android-maven](https://github.com/dcendents/android-maven-gradle-plugin) plugin.

If using Gradle 2.4:
 1. Add `classpath 'com.github.dcendents:android-maven-gradle-plugin:1.3'` to root build.gradle under `buildscript { dependencies {`
 2. Add the following lines to your library/build.gradle  
 ```
 apply plugin: 'com.github.dcendents.android-maven'  
 
 group='com.github.YourUsername'
 ```

After these changes go to the root of your project and run:

    ./gradlew install
    
It will install your library in your local maven repository ($HOME/.m2/repository).
If install works and you have added a GitHub release it should work jitpack.io

Please check which version of android-maven plugin is required for your Gradle version.  

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

Note: do not add the jitpack.io repository under `buildscripts` 

## Adding a sample app 

If you add a sample app to the same repo then your app needs to depend on the library. To do this in your app/build.gradle add a dependency in the form:

```gradle
dependencies {
    compile project(':library')
}
```

where 'library' is the name of your library module.

## Other notes

- By default the android-maven plugin generates an 'aar' file from your library. If you want to have a 'jar' instead take a look at the example project's library/build.gradle.
- Android NDK builds are not yet supported on JitPack
