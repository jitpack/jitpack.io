# API 

The base url for API calls is `https://jitpack.io/api`.

## Builds

Get all builds for a project and build outcomes.

**GET** `/builds/:groupId/:artifactId`

For example, the project https://github.com/jitpack/maven-simple will have the path:
`/builds/com.github.jitpack/maven-simple`

and a full url:
```
curl https://jitpack.io/api/builds/com.github.jitpack/maven-simple
```

Output:
```json
{
  "com.github.jitpack" : {
    "maven-simple" : {
      "1.1" : "ok",
      "1.0" : "ok",
      "0.5" : "Error",
      "0.1" : "ok"
    }
  }
}
```

Builds are ordered by time when they were executed.

## Single build

Get a single build for a project and it's outcome.

**GET** `/builds/:groupId/:artifactId/:tag`

To delete a build and it's artifacts use:

**DELETE** `/builds/:groupId/:artifactId/:tag`

You need to be authenticated when deleting a build and your user needs to have push permissions to the git repository.
Note that you can only delete failed builds, snapshot builds or tag builds newer than 7 days. Older versions can't be deleted because there could be builds depending on those versions.

Example:
`/builds/com.github.jitpack/maven-simple/1.0`

## Latest build

Get the latest build by tag. Tags are compared according to semantic versioning.

**GET** `/builds/:groupId/:artifactId/latest`

Get the latest build that was successfull.

**GET** `/builds/:groupId/:artifactId/latestOk`

## Authentication

API for private repositories uses basic authentication using your authentication token as the **username**. You can find your token on https://jitpack.io/private.

```
curl -uTOKEN: https://jitpack.io/api/builds/:groupId/:artifactId/:tag  
```
