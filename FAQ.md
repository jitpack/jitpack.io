Frequently Asked Questions
-

**Can artifacts be deleted from JitPack?**

Public repository artifacts on JitPack are immutable after 7 days of publishing. You will see an indicator in the list of versions when a build becomes frozen (snowflake icon). Withing the first 7 days they can be re-built to fix any release issues. Even then we recommend creating a patch release instead.

JitPack will also keep hosting artifacts after the originating git repository is deleted. To delete a build you need to have git push permissions to your git repository.

**What happens if a tag or repository is deleted on GitHub?**

If the project was already built then JitPack will continue serving the existing artifacts. It will not rebuild the project at the new tag. 
In case you need to redo a release the best option is to create a new version on GitHub.

**How can I get the latest snapshot of a repository?**

In your build file set the version of your dependency to `anyBranch-SNAPSHOT`. This is usefull during development but we don't recommend to be used in production.

You can also customize how often you want Gradle to check for new snapshots - see [the documentation](https://docs.gradle.org/1.8-rc-1/userguide/dependency_management.html#sec:controlling_caching). 

**Can I use JitPack with private repositories?**

Yes. See [private repositories](https://jitpack.io/private)

**Can I keep my source code private but make the library public?**

Yes. See [Artifact Sharing](https://jitpack.io/docs/PRIVATE/#artifact-sharing)

**Can I use my own domain name?**

Yes. We support mapping your domain name to your GitHub organization. Then instead of 'com.github.yourcompany' groupId you can use 'com.yourcompany'. 

Steps:

  1. Add a DNS TXT record: git.yourcompany.com -> https://github.com/yourcompany
  2. Go to https://jitpack.io/#com.yourcompany/yourrepo and click Look up. If DNS resolution worked then you should see a list of versions. 
  3. Select the version you want and click 'Get it' to see Maven/Gradle instructions.

Example: https://jitpack.io/#io.jitpack/gradle-simple

**Why am I getting `failed to resolve` error in Gradle?**

There could could be a number of reasons so we need to find the cause of this error.
The first thing to check is if the build was successfull by doing a Look Up on https://jitpack.io. 

To get more details run Gradle from command line with `--info --refresh-dependencies` flags.
The output should contain a line "HTTP Could not get" with the full URL and HTTP Status Code.

Possible reasons:
1. 404 - File not found. Build failed, tag does not exist or there is no such file in build artifacts.
2. 401 - Unauthorized. No token was supplied.
3. 403 - Forbidden. The token doesn't have access to the Git repository.

To re-authorize JitPack for private repositories:
1. Sign out of JitPack
2. Revoke JitPack on https://github.com/settings/applications
3. Authorize on https://jitpack.io/auth

If the error is unclear, feel free to contact Support.

**Can I use JitPack with my self-hosted GitLab server?**

Yes. Register your server in your [user page](https://jitpack.io/w/user)

**Can I use tag folders?**

Yes. Tag folders such as `feature/abc` are supported. Set the dependency version as `feature~abc`.

**Can I use branches with slashes in them?**

Yes. Branch names such as `branch/abc` are supported. Set the dependency version as `branch~abc`.

**Will my builds be reproducible?**

Absolutely. Once JitPack builds a project it keeps the build artifacts (jar, aar, ... files) and continues to serve those for all subsequent requests.

JitPack encourages reproducible builds in general since you need to have a working build file in order to publish artifacts. See also [Reproducible Build](http://martinfowler.com/bliki/ReproducibleBuild.html) article by Martin Fowler.

Note that -SNAPSHOT version will always provide the latest build therefore its only recommended during development and not in production.

**How are the artifacts you build licensed?**

Build artifact licenses are specified in the originating source code repositories. 

**Is JitPack like depending on source code repositories in other languages?**

Not really. With JitPack you specify which exact version you want and JitPack builds it. The author of the repository controls when to release a new version using GitHub's releases so from a consumer's perspective it's a typical package repository. 

**How are the builds secured?**

Each project is built in its own Docker container that only has access to the project's source code. It doesn't have access to other projects or build artifacts. Containers run only with normal user privileges (non root). 

All communication between our servers is VPN secured and files produced by the build are served over HTTPS (only).

Private repository builds are protected by authentication and require an access token.

If you'd like to report a security issue please contact security@jitpack.io

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

**How do I solve `peer not authenticated` error in Gradle?**

If you are running Gradle on Linux you might get the `peer not authenticated` error. There are at least two ways to solve this:
 - Upgrade to Gradle 2.11 or newer
 - Run Gradle with Java 8. The project itself doesn't need to use Java 8.

**Can I publish an existing .jar or .aar file?**

You can but the recommended way is always to build from source.

Sometimes you already have an existing artifact (.aar,.jar) as your dependency. For example, it may be provided by a third party without the source so you can't build it on JitPack.

There are a couple of ways of dealing with this:
  1. Use Gradle Shadow or Maven Shade plugin to embed the third party library into your own library
  2. Use custom commands on JitPack to publish the dependency: https://gist.github.com/jitpack-io/f928a858aa5da08ad9d9662f982da983
  
With option 2. the third party artifact becomes available as a Gradle/Maven dependency on JitPack.

**Does JitPack provide artifact checksums and signing**

JitPack creates sha and md5 checksums for all artifacts.
Artifact signing is not yet available however we are planning to add it as well.

**How do I resolve `Read timed out` error in Gradle?**

Since version 4.3 Gradle has reduced http timeouts which can cause downloads to time out when JitPack waits for a build to finish.
To increase timeouts add these settings to your gradle.properties file:
```
systemProp.org.gradle.internal.http.connectionTimeout=180000
systemProp.org.gradle.internal.http.socketTimeout=180000
```

**Where do I find invoices for my JitPack Subscription?**

Invoices are available on your user page - Sign In and click on your username (https://jitpack.io/w/user).
You can also receive invoices by email if you add an email address on your user page. 

**Change my repository to public but still got the message `No access token`**

When JitPack detects a private repository it caches this result for 1 hour. So, after change your repository to public you still need to wait 1 hour to be able to access.

[jitpack.io/issues/986](https://github.com/jitpack/jitpack.io/issues/986#issuecomment-265189883)

**Other questions**

Contact Support or open an [issue on GitHub](https://github.com/jitpack/jitpack.io/issues)
