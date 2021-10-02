# [101] Quickstart Containerized Java application 
This repository is a quickstart guide for building a simple Java SpringBoot application into a container image using Gradle, maven-jib-plugin.  Local tests are enabled by Docker & Minikube.

## What you will need?
* Some Software Development experience with Java, Docker, Kubernetes
* [Java](https://openjdk.java.net/install/) 11+
* [Gradle](https://gradle.org/install/) 7+
* [Docker](https://docs.docker.com/get-docker/) (for local build)
* [Minikube](https://minikube.sigs.k8s.io/docs/start/) (for local testing)
* A Github public repo (for CI)

## What you will learn?
1. **Build:** Build a container image for a Java Springboot app using `maven-jib-plugin`
2. **Run:** Run the container image in Kubernetes (Minikube), Gotchas in the Minikube / Docker setup
3. **Github Workflows:** build container image, publish Junit test results as Artifacts 

## Quickstart
### Build 
#### Build JAR file & run Junit tests
```
./gradlew clean test
```
#### Build Container Image (using Docker)
```
./gradlew clean test jibDockerBuild
```
#### Build Container Image (for CI/CD pipelines)
```
./gradlew clean test jib
```

### Run
#### Minikube / Docker
```
# !! Important Note !!
# Minikube comes with its own docker daemon and won't be able to find your local images by default

# 1. Start afresh
minikube delete
minikube start --driver=docker

# 2. Set environment variables (this is important)
eval $(minikube docker-env)

# 3. Build the container image
./gradlew clean test jibDockerBuild

# 4. Create deployment
kubectl run novarasa-java-pod --image=novarasa/quickstart-java-springboot --image-pull-policy=Never

# 5. See status of deployment & pods
kubectl get pods

# 5. On a separate terminal (to launch the Dashboard)
minikube dashboard

```

## Changes required in an Enterprise setup
Within an Enterprise, you wouldn't typically be directly using the online Maven Repository (or) Docker Hub to pull / push artifacts. So some modifications to the gradle configurations will be required.
* `gradle/gradle-wrapper.properties` - amend `distributionUrl` to point to Gradle distributions available in your enterprise's artifact repository (JFrog Artifactory / Sonatype Nexus)
* `build.gradle` - `jib.from.image` `jib.to.image` should point to fully qualified paths in your enterprise's container registry and `jib.from.auth` `jib.to.auth` should the developer / API credentials used to pull / push images. Do not hardcode credentials instead pass them as environment variables from your CI pipeline.


## References
* https://github.com/claudioaltamura/springboot-jib-helloworld
* https://spring.io/guides/gs/testing-web/ 
* https://github.com/marketplace/actions/publish-unit-test-results
* https://github.com/actions/starter-workflows/issues/171 (gradlew chmod)
* https://medium.com/bb-tutorials-and-thoughts/how-to-use-own-local-doker-images-with-minikube-2c1ed0b0968