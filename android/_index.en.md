---
title: Android
weight: 10
pre: "<b>3. </b>"
chapter: true
---

# Publish an Android library 

To publish your Android library on JitPack you just need a working build file in your Git repository.

Android SDK is available in the build environment and ANDROID_HOME variable is already set when the build starts.
Builds are run with Java 8 by default but can be configured using a jitpack.yml file.

## Gradle

To build and publish your library on JitPack you need the `maven-publish` plugin as explained in [the Android documentation](https://developer.android.com/studio/build/maven-publish-plugin).

1. Add the plugin:

```gradle
plugins {
    id 'maven-publish'
}
```

2. Configure publishing

```gradle
publishing {
    publications {
        release(MavenPublication) {
            groupId = 'io.jitpack'
            artifactId = 'library'
            version = '1.0'

            afterEvaluate {
                from components.release
            }
        }
    }
}
```

## Checks

Check that your library can be installed to mavenLocal (`$HOME/.m2/repository`):

```
./gradlew publishToMavenLocal

// or if you named your publication "release"
./gradlew publishReleasePublicationToMavenLocal
```

## Create your release

If everything went well in the previous step, your library is ready to be released! Create a GitHub release or add a git tag and you're done!

## Installing

Users of your library will need to add the jitpack.io repository to **settings.gradle** file:

```gradle
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        google()
        mavenCentral()
        maven { url 'https://jitpack.io' }
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

- [Library example](https://github.com/jitpack/android-example) 

