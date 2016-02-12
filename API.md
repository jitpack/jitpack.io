# API

The base url for api calls is `https://jitpack.io/api`.

API for private repositories uses basic authentication. Pass your authentication token as the username.

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

Example:
`/builds/com.github.jitpack/maven-simple/1.0`

## Latest build

Get the latest build by tag. Tags are compared according to semantic versioning.

**GET** `/builds/:groupId/:artifactId/latest`

Get the latest build that was successfull.

**GET** `/builds/:groupId/:artifactId/latestOk`

