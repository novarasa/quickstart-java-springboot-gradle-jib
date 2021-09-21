# Java-Gradle-ContainerImage Quickstart
Quickstart repository to build a containerized Java application using Gradle & Jib

## What you will need
### Build
* Java 11+
* Gradle 7+
* Docker (for desktop builds only)

## Quickstart
### Build JAR file & run Junit tests
```
./gradlew clean test
```
### Build Container Image (using Docker)
```
./gradlew clean test jibDockerBuild
```
### Build Container Image (for CI/CD pipelines)
```
./gradlew clean test jib
```

## Changes required in an Enterprise setup
Within an Enterprise, you wouldn't typically be directly using the online Maven Repository (or) Docker Hub to pull / push artifacts. So some modifications to the gradle configurations will be required.
* `gradle#gradle-wrapper.properties` - amend `distributionUrl` to point to Gradle distributions available in your enterprise's artifact repository (JFrog Artifactory / Sonatype Nexus)
* `build.gradle` - `jib.from.image` `jib.to.image` should point to fully qualified paths in your enterprise's container registry and `jib.from.auth` `jib.to.auth` should the developer / API credentials used to pull / push images. Do not hardcode credentials instead pass them as environment variables from your CI pipeline.


## References
* https://github.com/claudioaltamura/springboot-jib-helloworld
* https://spring.io/guides/gs/testing-web/ 
* https://github.com/marketplace/actions/publish-unit-test-results