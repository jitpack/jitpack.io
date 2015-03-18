# jitpack.io

This is a repository for documentation and issues of https://jitpack.io service

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jitpack/jitpack.io?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

About
======

JitPack is an easy to use package repository for JVM projects. It builds GitHub projects on demand and provides you with ready-to-use packages.

How to
======

To get a GitHub project into your build:

**Step 1.** Add the JitPack maven repository to your build file

```groovy
    url "https://jitpack.io"
```

**Step 2.**  Add the dependency in the form:

 - *Group:* com.github.Username
 - *Artifact:* Repository Name
 - *Version:* Release tag or commit id
  
**That's it!** The first time you request a project JitPack checks out the code, builds it and sends the Jar files back to you.

See the [Guide to building](https://github.com/jitpack/jitpack.io/blob/master/BUILDING.md) for more details and instructions on building multi-module projects.

If the project doesn't have any [GitHub Releases](https://github.com/blog/1547-release-your-software) you can get the latest snapshot build. In this case use the short commit id as the version.

Releasing on JitPack
======

Releasing your library on JitPack is extremely simple. 

**Step 1**: Create a [GitHub Release](https://github.com/blog/1547-release-your-software)  
**That's it**

As long as three's a build file in your repository and it can install your library in the local Maven repository, it is sufficient for JitPack.

Some extra things to consider:

- Add dependency information. Tell the world where to get your library: 
 
   ```gradle
   repositories { 
        maven { url "https://jitpack.io" }
   }
   dependencies {
         compile 'com.github.jitpack:gradle-simple:1.0'
   }
   ```  
It's easy to look up the dependency information on https://jitpack.io. Just paste your GitHub url and press Look Up
   
- Add sources jar. Creating the sources jar makes it easier for others to use your code and contribute.
- Add a badge. You can add a version badge to your readme.md, for example:

[![Release](https://img.shields.io/github/release/jitpack/gradle-simple.svg?label=maven)](https://jitpack.io/#jitpack/gradle-simple)

```
[![Release](https://img.shields.io/github/release/jitpack/gradle-simple.svg?label=maven)](https://jitpack.io/#jitpack/gradle-simple)
```

- Show up-to-date version in HTML. If your project has a website you can get and display the latest release using JavaScript and GitHub API: https://gist.github.com/jitpack-io/5bd698d35303b2c370a0

Other Features
======
- Javadoc publishing. If the project produces a javadoc.jar then you can browse the javadoc files directly at: 
    - `https://jitpack.io/com/github/USER/REPO/VERSION/javadoc/`   
- Finds build files in sub-folders if there is no build file at the root of the repository

Motivation
======

There are a lot of great libraries on GitHub but unfortunately many of them are not published on any public repositories. You could always check out the code, build and deploy locally:

 - [Can I use a GitHub project directly in Maven?](http://stackoverflow.com/q/8871056/1180621) question on StackOverflow

but wouldn't it be great if the library was already built and available to use? Well now it is.

With JitPack all the author needs to do is create a [GitHub Release](https://github.com/blog/1547-release-your-software) and the project becomes available for everyone to use. So sharing releases is simpler for authors as well.



