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

## References
* https://github.com/claudioaltamura/springboot-jib-helloworld
* https://spring.io/guides/gs/testing-web/ 
* https://github.com/marketplace/actions/publish-unit-test-results