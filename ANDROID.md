# Publish an Android library 

In order to publish your Android library on JitPack you just need a working build file in your Git repository.

Android SDK is available in the build environment and ANDROID_HOME variable is already set when the build starts.
Builds are run with Java 8 by default but can be configured using a jitpack.yml file.

## Gradle

To enable building on JitPack you need to configure the `maven-publish` Gradle plugin to publish your library as explained in [the Android documentation](https://developer.android.com/studio/build/maven-publish-plugin).

## Checks

Check that your library can be installed to mavenLocal (`$HOME/.m2/repository`):

```
./gradlew publishToMavenLocal

// or if you named your publication "release"
./gradlew publishReleasePublicationToMavenLocal
```

## Create your release

If everything wen well in the previous step, your library is ready to be released! Create a GitHub release or add a git tag and you're done!

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
    implementation 'com.github.jitpack:android-example:1.0.1'
}
```

Note: do not add the jitpack.io repository under `buildscript` 

## Adding a sample app 

If you add a sample app to the same repo then your app needs to depend on the library. To do this in your app/build.gradle add a dependency in the form:

```gradle
dependencies {
    implementation project(':library')
}
```

where 'library' is the name of your library module.

## Examples

- [Library example](https://github.com/jitpack/android-sample) 

