Frequently Asked Questions
-

**What happens if a tag or repository is deleted on GitHub?**

If the project was already built then JitPack will continue serving the existing artifacts. It will not rebuild the project at the new tag. 
In case you need to redo a release the best option is to create a new version on GitHub.

**Can I use JitPack with private repositories?**

Yes. See [private repositories](https://jitpack.io/private)

**How can I get the latest snapshot of a repository?**

In your build file set the version of your dependency to `-SNAPSHOT`. This is usefull during development but we don't recommend to be used in production.

You can also customize how often you want Gradle to check for new snapshots - see [the documentation](https://docs.gradle.org/1.8-rc-1/userguide/dependency_management.html#sec:controlling_caching). 

**Can I use my own domain name?**

Yes. We support mapping your domain name to your GitHub organization. Then instead of 'com.github.yourcompany' groupId you can use 'com.yourcompany'. 

Steps:

  1. Add a DNS TXT record: git.yourcompany.com -> https://github.com/yourcompany
  2. Go to https://jitpack.io/#com.yourcompany/yourrepo and click Look up. If DNS resolution worked then you should see a list of versions. 
  3. Select the version you want and click 'Get it' to see Maven/Gradle instructions.

Example: https://jitpack.io/#io.jitpack/gradle-simple

**Will my builds be reproducible?**

Absolutely. Once JitPack builds a project it keeps the build artifacts (jar, aar, ... files) and continues to serve those for all subsequent requests.

JitPack encourages reproducible builds in general since you need to have a working build file in order to publish artifacts. See also [Reproducible Build](http://martinfowler.com/bliki/ReproducibleBuild.html) article by Martin Fowler.

Note that -SNAPSHOT version will always provide the latest build therefore its only recommended during development and not in production.

**How are the artifacts you build licensed?**

Build artifacts licenses are specified in the originating source code repositories. 

**Is this like depending on source code repositories in other languages?**

Not really. With JitPack you specify which exact version you want and JitPack builds it. The author of the repository controls when to release a new version using GitHub's releases so from a consumer's perspective it's a typical package repository. 

**How are the builds secured?**

Each project is built in its own Docker container that only has access to the project's source code. It doesn't have access to other projects or build artifacts. Containers run only with normal user privileges (non root). 

All communication between our servers is VPN secured and files produced by the build are served over HTTPS (only).

Private repository builds are protected by authentication and require an access token.

**Can I rebuild my project?**

If your first build wasn't successfull you can rebuild it. If you Sign In on JitPack.io then you'll be able to remove the old build and re-requesting it will trigger a new build. 

See also https://jitpack.io/docs/BUILDING/#rebuilding

**Can version ranges be used with JitPack?**

You can use version ranges and Gradle's dynamic versions for releases. Currenly they only resolve to releases that have been built.
`compile 'com.github.User:Repo:1.+'`

**How long can builds take?**

Up to 15 minutes

**Is JitPack similar to Maven Central?**

JitPack is a public maven repository and serves maven artifacts. In that sense it is similar to Maven Central. However, JitPack takes a completely different approach to how you get your artifacts in the repository. With Maven Central you build the artifacts yourself and then upload them. With JitPack you create a git tag for a release and it will build the artifacts from source.

**Other questions**

Send them to jitpack at jitpack.io or come to https://gitter.im/jitpack-io
