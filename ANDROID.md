# Publish an Android library 

In order to publish your Android library on JitPack you just need a working build file in your Git repository.

Android SDK is available in the build environment and ANDROID_HOME variable is already set when the build starts.
Builds are run with Java 8 by default but can be configured using a jitpack.yml file.

## Gradle

To enable building on JitPack you need to add the [android-maven](https://github.com/dcendents/android-maven-gradle-plugin) plugin. 

If using Gradle *4.6* or later:

1) In your root build.gradle: 
```gradle
buildscript { 
  dependencies {
    classpath 'com.github.dcendents:android-maven-gradle-plugin:2.1' // Add this line
``` 

2) In your library/build.gradle add:  

```gradle
 apply plugin: 'com.github.dcendents.android-maven'  
 
 group='com.github.YourUsername'
```

3) Create a GitHub release or add a git tag.

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

## Jar file

By default the android-maven plugin generates an 'aar' file from your library. If you want to have a 'jar' instead take a look at the [Example](https://github.com/jitpack/android-example) project's library/build.gradle.

# Tutorials

 - [How to create an Android Gradle library (with video)](https://medium.com/@levibostian/how-to-create-an-android-gradle-library-cf2792b39be#.nkeke59zp) by Levi Bostian
 - [Publish an Android Library](https://medium.com/@ome450901/publish-an-android-library-by-jitpack-a0342684cbd0#.44sbcommx)
 - [Publishing Java / Android / Kotlin libraries](https://medium.com/@erluxman/publishing-java-android-kotlin-libraries-on-jitpack-b33d0d26dc8a)
 
