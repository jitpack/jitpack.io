# JitPack.io

This is a repository for documentation and issues of https://jitpack.io service

Need help setting up a repo? Come to  [![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jitpack/jitpack.io?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

About
======

JitPack is an easy to use package repository for JVM projects. It builds GitHub projects on demand and provides you with ready-to-use artifacts (jar, aar). The core idea is that in order to publish your library you don't need to build and upload it yourself. Just push your changes and create a GitHub release. Done!

How to
======

To get a GitHub project into your build:

**Step 1.** Add the JitPack maven repository to your build file

```gradle
    url "https://jitpack.io"
```

**Step 2.**  Add the dependency information:

 - *Group:* com.github.Username
 - *Artifact:* Repository Name
 - *Version:* Release tag or commit id
  
In Gradle that would be: `compile 'com.github.User:Repo:Tag'` 
  
**That's it!** The first time you request a project JitPack checks out the code, builds it and sends the Jar files back to you.

Too see an example head to https://jitpack.io and 'Look Up' a GitHub repository by url.

## Building

See also the [Guide to building](https://github.com/jitpack/jitpack.io/blob/master/BUILDING.md) for more details and for instructions on building multi-module projects.

If the project doesn't have any [GitHub Releases](https://github.com/blog/1547-release-your-software) you can get the latest snapshot build. In this case use the short commit id as the version. You can also place tags on other branches and then build using those tags.

## BitBucket

Using BitBucket is similar to using GitHub repositories. The only difference is:
 - *Group:* org.bitbucket.Username

Too see an example head to https://jitpack.io and 'Look Up' a BitBucket repository by url.

Releasing on JitPack
======

Releasing your library on JitPack is very simple. 

- Create a [GitHub Release](https://github.com/blog/1547-release-your-software)  

As long as there's a build file in your repository and it can install your library in the local Maven repository, it is sufficient for JitPack.

*Tip:* You can automate GitHub releases with [Gradle release & version management plugin](https://github.com/allegro/axion-release-plugin)

### Some extra things to consider:

- Add dependency information in your README. Tell the world where to get your library: 
 
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

- Show up-to-date version in HTML. If your project has a website or GitHub pages then you can display the latest release using JavaScript: https://gist.github.com/jitpack-io/5bd698d35303b2c370a0

Other Features
======
- Javadoc publishing. If the project produces a javadoc.jar then you can browse the javadoc files directly at: 
    - `https://jitpack.io/com/github/USER/REPO/VERSION/javadoc/`   
- Private repositories https://jitpack.io/private
- Dynamic versions. You can youse Gradle's dynamic version '1.+' and Maven's version ranges for releases. They resolve to releases that have already been built.
- Build by tag and by commit id.
- Finds build files in sub-folders if there is no build file at the root of the repository

Motivation
======

There are a lot of great libraries on GitHub but unfortunately many of them are not published on any public repositories. You could always check out the code, build and deploy locally:

 - [Can I use a GitHub project directly in Maven?](http://stackoverflow.com/q/8871056/1180621) question on StackOverflow

but wouldn't it be great if the library was already built and available to use? Well now it is.

With JitPack all the author needs to do is create a [GitHub Release](https://github.com/blog/1547-release-your-software) and the project becomes available for everyone to use. So sharing releases is simpler for authors as well.

Other
======

See the [FAQ page](FAQ.md)
