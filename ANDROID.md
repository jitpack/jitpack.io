# Publish an Android library 

In order to publish your Android library on JitPack you just need a working build file in your Git repository.

Android SDK is available in the build environment and ANDROID_HOME variable is already set when the build starts.
Builds are run with Java 7 by default.

## Gradle

To enable building on JitPack you need to add the [android-maven](https://github.com/dcendents/android-maven-gradle-plugin) plugin. 

If using Gradle *2.4* or later:

1) In your root build.gradle: 
```gradle
buildscript { 
  dependencies {
    classpath 'com.github.dcendents:android-maven-gradle-plugin:1.3' // Add this line
``` 

2) In your library/build.gradle add:  

```gradle
 apply plugin: 'com.github.dcendents.android-maven'  
 
 group='com.github.YourUsername'
```

3) Create a GitHub release or add a tag.

## Checks

Check that you have the [Gradle wrapper](https://docs.gradle.org/current/userguide/gradle_wrapper.html) in your Git repository. If you don't then create it using the command `gradle wrapper` and commit it. Also check that the generated gradle-wrapper.jar is not ignored with .gitignore rules.

**Test**. After these changes go to the root of your project and run the Gradle wrapper with:

    ./gradlew install
    
It will install your library in your local maven repository ($HOME/.m2/repository). 
If install works and you have added a GitHub release it should work jitpack.io

**Important:** Please check [here](https://github.com/dcendents/android-maven-gradle-plugin#note-on-releases) which version of android-maven plugin is required for your Gradle version. Your Gradle version is specified in gradle/wrapper/gradle-wrapper.properties file.    

## Examples

- [Android-Example](https://github.com/jitpack/android-example) 

- [Multiple build variants](https://github.com/jitpack-io/android-jitpack-library-example)

## Installing

Users of your library will need add the jitpack.io repository:

```gradle
allprojects {
 repositories {
    jcenter()
    maven { url "https://jitpack.io" }
 }
}
```

and:

```gradle
dependencies {
    compile 'com.github.jitpack:android-example:1.0.1'
}
```

Note: do not add the jitpack.io repository under `buildscript` 

## Adding a sample app 

If you add a sample app to the same repo then your app needs to depend on the library. To do this in your app/build.gradle add a dependency in the form:

```gradle
dependencies {
    compile project(':library')
}
```

where 'library' is the name of your library module.

## Other notes

- By default the android-maven plugin generates an 'aar' file from your library. If you want to have a 'jar' instead take a look at the [Example](https://github.com/jitpack/android-example) project's library/build.gradle.

