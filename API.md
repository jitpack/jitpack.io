# API (Beta)

The base url for api calls is `https://jitpack.io/api`.

## Builds

Get all builds for a project and build outcomes.

**GET** `/builds/:groupId/:artifactId`

Example:
`/builds/com.github.jitpack/maven-simple`

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

## Single build

Get a single build for a project and it's outcome.

**GET** `/builds/:groupId/:artifactId/:tag`

To delete a build and it's artifacts use:

**DELETE** `/builds/:groupId/:artifactId/:tag`

You need to be authenticated when deleting a build and your user needs to have push permissions to the git repository.

Example:
`/builds/com.github.jitpack/maven-simple/1.0`

## Latest build

Get the latest build by tag. Tags are compared according to semantic versioning.

**GET** `/builds/:groupId/:artifactId/latest`

Get the latest build that was successfull.

**GET** `/builds/:groupId/:artifactId/latestOk`

## Authentication

API for private repositories uses basic authentication. Pass your authentication token as the username.

```
curl -uTOKEN: https://jitpack.io/api/builds/:groupId/:artifactId/:tag  
```
