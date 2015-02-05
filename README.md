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
 - *Version:* Release tag
  
**That's it!** The first time you request a project JitPack checks out the code, builds it and sends the Jar files back to you.

If the project doesn't have any [GitHub Releases](https://github.com/blog/1547-release-your-software) you can get the latest snapshot build. In this case use the version they have in their pom.


Why
======

There are a lot of great libraries on GitHub but unfortunately many of them are not published on any public repositories. You could always check out the code, build and deploy locally:

 - [Can I use a GitHub project directly in Maven?](http://stackoverflow.com/q/8871056/1180621) question on StackOverflow

but wouldn't it be great if the library was already built and available to use? Well now it is.

With JitPack all the author needs to do is create a [GitHub Release](https://github.com/blog/1547-release-your-software) and the project becomes available for everyone to use. So sharing releases is simpler for authors as well.



