# Guide to building projects

JitPack currently can build **Gradle**, **Maven** and **Sbt** projects. Support for other build frameworks is coming later on.

If the project has a build.gradle file then it will be built using Gradle otherwise JitPack will look for a pom.xml or a build.sbt file. The build.gradle file can also be located in a subfolder.

## Gradle projects

Projects using Gradle need to have either the [maven](http://gradle.org/docs/current/userguide/maven_plugin.html) or [maven-publishing](https://gradle.org/docs/current/userguide/publishing_maven.html) plugin enabled. For example, if you add this line to your build file:

```gradle
    apply plugin: 'maven'
```

then JitPack will run:

```gradle
    gradle install
```

to install the jar and pom file in it's local maven repository. With maven-publishing plugin it will run `gradle publishToMavenLocal`. If your projects uses the gradle wrapper JitPack will run ./gradlew.

### Example projects

 - Simple - https://github.com/jitpack/gradle-simple
 - Multiple modules - https://github.com/jitpack/gradle-modular
 - Project with multiple artifacts - https://github.com/jitpack/gradle-multiple-jars

## Android projects

See the [Guide to building Android projects](https://github.com/jitpack/jitpack.io/blob/master/ANDROID.md) with Gradle

## Maven projects

JitPack will run: 

    mvn install -DskipTests
    
to build and publish Maven projects. 

### Example projects

 - Simple - https://github.com/jitpack/maven-simple
 - Multiple modules - https://github.com/jitpack/maven-modular
  
# Multi-module projects

If the project builds multiple modules JitPack will append the repository name to the artifact's groupId and the module's name will stay in the artifactId. It will also generate a module that includes all of repository's modules as dependencies. That way if you don't know which module you want you can get all of them by adding just a single dependency to your build file.

To get individual artifacts of multi-module builds use `com.github.User.Repo` as group Id and `ModuleName` as the artifact Id.

Individual module in Gradle:

```gradle
compile 'com.github.User.Repo:Module:Tag'
```
or in Maven:

```xml
<dependency> 
	<groupId>com.github.User.Repo</groupId> 
	<artifactId>Module</artifactId> 
	<version>Tag</version> 
</dependency>
``` 

To get all modules of a project use the standard syntax:
```gradle
compile 'com.github.User:Repo:Tag'
```

Examples:
 - Multiple Gradle modules - https://github.com/jitpack/gradle-modular
 - Multiple Maven modules - https://github.com/jitpack/maven-modular

## Sbt projects

JitPack can build sbt projects and also provide dependencies to sbt. 
When building an Sbt project JitPack will run:

    sbt publishM2

To use JitPack repository from sbt add this to build.sbt:
```sbt
resolvers += "jitpack" at "https://jitpack.io"
```
and then use:
```sbt
libraryDependencies += "com.github.User" % "Repo" % "Tag"
```

# Java version

JitPack will compile projects using Oracle Java 8. See the example projects on how to set a different target version.

# Troubleshooting

If there is an issue with a build you will see a link to the log in the Status column. You can also inspect the build log for any other build using the URL:

```
https://jitpack.io/com/github/User/Repo/Tag/build.log
```

and it sometimes helps to look at the pom file itself:

```
curl -v https://jitpack.io/com/github/User/Repo/Tag/Repo-Tag.pom
```

Although we monitor all the builds feel free to get in touch any time you face an issue. 
The easiest way is to open a GitHub issues or come chat on https://gitter.im/jitpack-io
