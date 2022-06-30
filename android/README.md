https://hub.docker.com/r/lizhaotailang/gitlab-runner-android/

This Docker image contains Android SDK (version 30 with build-tools 30.0.2) and some necessary packages for building Android apps in CI environment (GitLab CI as a typical example).

Cache should be **enabled** to speed up builds.

An example `.gitlab-ci.yml` would look like this:

```yml
image: lizhaotailang/gitlab-runner-android

stages:
  - build

before_script:
  - export GRADLE_USER_HOME=$(pwd)/.gradle
  - chmod +x ./gradlew

cache:
  key: ${CI_PROJECT_ID}
  paths:
    - .gradle/

build:
  stage: build
  script:
    - ./gradlew assembleRelease
```
