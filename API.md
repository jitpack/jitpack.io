# API

## Builds

Get all builds for a project and build outcomes.

GET `/api/builds/:groupId/:artifactId`

Example:
`/api/builds/com.github.jitpack/maven-simple`

Output:
```json
{
  "com.github.jitpack" : {
    "maven-simple" : {
      "1.1" : "ok",
      "1.0" : "ok",
      "0.1" : "Error",
      "0.1" : "ok"
    }
  }
}
```
