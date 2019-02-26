JitPack.io
=====
JitPack is a novel package repository for JVM and Android projects. It builds Git projects on demand and provides you with ready-to-use artifacts (jar, aar).

If you want your library to be available to the world, there is no need to go through project build and upload steps. All you need to do is push your project to GitHub and JitPack will take care of the rest. That’s really it!

In case your project is already on GitHub, JitPack makes sure it can be built by anyone. Want to use a GitHub library in your project? Follow the simple steps explained in the ‘Building with JitPack’ section.

For issues and enhancements, please use the [JitPack GitHub repository](https://github.com/jitpack/jitpack.io/). The repository contains this documentation and contributions are welcome there as well.

If you'd like some help with setting up repositories please use the Support button on the web site. 

Building with JitPack
=====

If you are using Gradle to get a GitHub project into your build, you will need to:

**Step 1.** Add the JitPack maven repository to the list of repositories:

```gradle
    url "https://jitpack.io"
```

**Step 2.**  Add the dependency information:

 - *Group:* com.github.Username
 - *Artifact:* Repository Name
 - *Version:* Release tag, commit hash or `-SNAPSHOT`

**That's it!** The first time you request a project JitPack checks out the code, builds it and sends the Jar files back to you.

To see an example head to [jitpack.io](https://jitpack.io) and 'Look Up' a GitHub repository by url.

Gradle example:
```gradle
    allprojects {
        repositories {
            jcenter()
            maven { url "https://jitpack.io" }
        }
   }
   dependencies {
        implementation 'com.github.User:Repo:Version'
   }
```

*Note*: when using multiple repositories in build.gradle it is recommended to add JitPack *at the end*. Gradle will go through all repositories in order until it finds a dependency.

**Snapshots**

Snapshot versions are useful during development. A snapshot is a version that has not been released. The difference between a real version and a snapshot is that snapshot might still get updates. Snapshot versions are useful during development process and JitPack provides two ways to get them. You can specify a version for your dependency as:

 - commit hash

 - `branch-SNAPSHOT` (replace 'branch' with any branch name, e.g. master)

For example:
```gradle
    // dependency on the latest commit in the master branch
    implementation 'com.github.jitpack:gradle-simple:master-SNAPSHOT'
```

Adding `-SNAPSHOT` will build the latest commit on the master branch.

Gradle can cache the SNAPSHOT builds. You could add the following configuration in your build.gradle file in order to ensure Gradle always picks up the 'freshest' version of the build:

```gradle
configurations.all {
    resolutionStrategy.cacheChangingModulesFor 0, 'seconds'
}
```

Or you could also run Gradle from the command line with the `--refresh-dependencies` flag. See the [Gradle documentation](https://docs.gradle.org/2.5/userguide/dependency_management.html#changing-module-cache-control) for more information on how to configure caching for *changing* dependencies.

*Note* If using Android Studio, don't forget to press File->Synchronize after updating to a newer snapshot.

Also see the [Guide to building](BUILDING.md) for more details and instructions on building multi-module projects.

If the project doesn't have any [GitHub Releases](https://github.com/blog/1547-release-your-software), you can get the latest snapshot build. In this case, use the short commit id as the version. You can also place tags on other branches and then build using those tags.

*Tip:* You can also automate GitHub releases with [Gradle release & version management plugin](https://github.com/allegro/axion-release-plugin)


Publishing on JitPack
======

Publishing your library on JitPack is very simple:

- Create a [GitHub Release](https://github.com/blog/1547-release-your-software)  

As long as there's a build file in your repository and it can install your library in the local Maven repository, it is sufficient for JitPack. See the [Guide to building](BUILDING.md) on how to publish JVM libraries and [Guide to Android](ANDROID.md) on how to publish Android libraries.

*Tip:* You can try out your code before a release by using the commit hash as the version.

**Some extras to consider**

Add dependency information in your README. Tell the world where to get your library:

```gradle
   repositories {
        jcenter()
        maven { url "https://jitpack.io" }
   }
   dependencies {
         implementation 'com.github.jitpack:gradle-simple:1.0'
   }
```  

- Add sources jar. Creating the sources jar makes it easier for others to use your code and contribute.


# Features #

## Javadoc publishing ##

- For a single module project, if it produces a javadoc.jar then you can browse the javadoc files directly at: 
    - `https://jitpack.io/com/github/USER/REPO/VERSION/javadoc/` or
    - `https://jitpack.io/com/github/USER/REPO/latest/javadoc/` (latest release tag)

- For a multi module project, the artifacts are published under `com.github.USER.REPO:MODULE:VERSION`, where `MODULE` is the artifact id of the module (not necessarily the same as the directory it lives in)

- Javadocs for a multi-module project follow the same convention, i.e.

    - `https://jitpack.io/com/github/USER/REPO/MODULE/VERSION/javadoc/` 

- Aggregated javadocs for a multi-module project may be available if the top level aggregates them into a jar and publishes it. The module name in this case is the artifact id of the top level module.

- See the example projects on how to configure your build file ([Android example](https://github.com/jitpack/android-example/blob/master/library/build.gradle)). 

## Other features #

- [Private repositories](https://jitpack.io/private)
- Dynamic versions. You can use Gradle's dynamic version '1.+' and Maven's version ranges for releases. They resolve to releases that have already been built. JitPack periodically checks for new releases and builds them ahead-of-time.
- Build by tag, commit id, or `anyBranch-SNAPSHOT`.
- You can also use your own domain name for groupId
- Immutable artifacts. Builds cannot be changed after 7 days

## Other Git hosts ##

JitPack also works with other Git hosting providers. The only difference is the groupId of your artifacts:

 - BitBucket: *org.bitbucket*.Username:Repo:Tag

 - GitLab: *com.gitlab*.Username:Repo:Tag
 
 - Gitee: *com.gitee*.Username:Repo:Tag

To see an example, head to https://jitpack.io and 'Look Up' a Git repository by url.

Self-hosted Git servers like GitLab are also supported. You can register your server on your [user page](https://jitpack.io/w/user).

## Custom domain name ##

If you want to use your own domain name as the groupId instead of com.github.yourcompany, you can.
We support mapping your domain name to your GitHub organization. Then, instead of 'com.github.yourcompany' groupId, you can use 'com.yourcompany' while the name of the project and version remains the same.

To enable your own domain name:  

  1. Add a DNS TXT record that maps git.yourcompany.com to https://github.com/yourcompany. This needs to be configured at your domain name provider such as GoDaddy. For example see [How to add a TXT record](https://uk.godaddy.com/help/add-a-txt-record-19232).  

  2. Go to https://jitpack.io/#com.yourcompany/yourrepo and click Look up. If DNS resolution worked then you should see a list of versions.   

  3. Select the version you want and click 'Get it' to see Maven/Gradle instructions.  

Example: [https://jitpack.io/#io.jitpack/gradle-simple](https://jitpack.io/#io.jitpack/gradle-simple)

To check that the DNS TXT record was added, run the command `dig txt git.yourcompany.com`. For example:
```
~$ dig txt git.jitpack.io
...
;; ANSWER SECTION:
git.jitpack.io.		600	IN	TXT	"https://github.com/jitpack"
```

## Badges ##

Add this line to your README.md to show a status badge with the latest release:

```
[![Release](https://jitpack.io/v/User/Repo.svg)]
(https://jitpack.io/#User/Repo)
```


[![Release](https://jitpack.io/v/jitpack/maven-simple.svg)](https://jitpack.io/#jitpack/maven-simple)


If you are using a custom domain or BitBucket, use:

```
[![Release](https://jitpack.io/v/com.example/Repo.svg)]
(https://jitpack.io/#com.example/Repo)


[![Release](https://jitpack.io/v/org.bitbucket.User/Repo.svg)]
(https://jitpack.io/#org.bitbucket.User/Repo)
```

Or, if you prefer the flat-squared style:

```
https://jitpack.io/v/User/Repo.svg?style=flat-square
```

[![Release](https://jitpack.io/v/jitpack/maven-simple.svg?style=flat-square)](https://jitpack.io/#jitpack/maven-simple)


FAQ
======

See the [FAQ page](FAQ.md)
