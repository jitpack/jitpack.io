# Guide to building projects

JitPack currently can build Gradle and Maven projects. Support for other build frameworks is coming later on.

If the project has a pom.xml file then it will be built using Maven otherwise JitPack will look for a build.gradle file.


## Gradle projects

Projects using Gradle need to have either the [maven](http://gradle.org/docs/current/userguide/maven_plugin.html) or [maven-publishing](https://gradle.org/docs/current/userguide/publishing_maven.html) plugin enabled. For example, if you add this line to your build file:

```groovy
    apply plugin: 'maven'
```

then JitPack will run:

```
    gradle install
```

to install the jar and pom file in it's local maven repository. With maven-publishing plugin it will run `gradle publishToMavenLocal`. If your projects uses the gradle wrapper JitPack will run ./gradlew.

### Example projects

 - Simple - https://github.com/jitpack/gradle-simple
 - Multiple modules - https://github.com/jitpack/gradle-modular
 - Project with multiple artifacts - https://github.com/jitpack/gradle-multiple-jars

## Maven projects

JitPack will run: 

    mvn install 
    
to build and publish Maven projects. 

### Example projects

 - Simple - https://github.com/jitpack/maven-simple
 - Multiple modules - https://github.com/jitpack/maven-modular
  
# Multi-module projects

To get individual artifacts of multi-module builds use `Repo.ModuleName` as the artifact Id.

In Gradle:

```groovy
compile 'com.github.User:Repo.Module:Tag'
```
or in Maven:

```xml
<dependency> 
	<groupId>com.github.User</groupId> 
	<artifactId>Repo.Module</artifactId> 
	<version>Tag</version> 
</dependency>
``` 

# Java version

JitPack will compile projects using Java 8. See the example projects on how to set a different target version.

# Troubleshooting

If there is an issue with a build you will see a link to the log in the Status column. You can also inspect the build log for any other build using the URL:

```
https://jitpack.io/com/github/User/Repo/Tag/build.log
```

and it sometimes helps to look at the pom file itself:

```
curl https://jitpack.io/com/github/User/Repo/Tag/Repo-Tag.pom
```

Although we monitor all the builds feel free to get in touch any time you face an issue. 
