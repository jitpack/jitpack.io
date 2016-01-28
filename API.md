# API

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

Example:
`/builds/com.github.jitpack/maven-simple/1.0`

