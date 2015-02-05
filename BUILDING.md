
JitPack currently can build Gradle and Maven projects. Support for other build frameworks is coming later on.

Gradle projects
=============

Projects using Gradle need to have either the `maven` or `maven-publishing` plugin enabled. For example:

```groovy
    apply plugin: 'maven'
```

and JitPack will run:

```
    gradle install
```

## Example projects

 - Simple - https://github.com/jitpack/gradle-simple
 - Multiple modules - https://github.com/jitpack/gradle-modular
 - Project with multiple artifacts - https://github.com/jitpack/gradle-multiple-jars


Maven projects
=============

JitPack will run: 

    mvn install
    
to build and publish Maven projects. 
