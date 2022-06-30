FROM --platform=linux/amd64 ubuntu:20.04
LABEL maintainer TonnyL

ENV ANDROID_HOME "/opt/android-sdk-linux"
ENV PATH=$PATH:$ANDROID_HOME/platform-tools
ENV PATH=$PATH:$ANDROID_HOME/build-tools/$BUILD_TOOLS
ENV PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin

ENV DEBIAN_FRONTEND=noninteractive

ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk-amd64

ARG CMD_TOOLS="7583922"
ARG BUILD_TOOLS="30.0.2"
ARG TARGET_SDK="30"

ARG CMD_TOOLS_ZIP="/tmp/cmdlinetools.zip"
ARG CMD_TOOLS_DIR="${ANDROID_HOME}/cmdline-tools/latest/"

RUN apt-get -qq update && apt-get install -y locales \
        && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG en_US.UTF-8

RUN apt-get install -qqy --no-install-recommends \
    openjdk-11-jdk \
    unzip \
    git-core \
    wget && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget -q https://dl.google.com/android/repository/commandlinetools-linux-${CMD_TOOLS}_latest.zip -O ${CMD_TOOLS_ZIP} && \
    unzip -qq ${CMD_TOOLS_ZIP} -d /tmp/ && \
    mkdir -p ${CMD_TOOLS_DIR} && \
    mv /tmp/cmdline-tools/* ${CMD_TOOLS_DIR} && \
    rm -v ${CMD_TOOLS_ZIP}

RUN mkdir -p ~/.android/ && touch ~/.android/repositories.cfg && \
    yes | sdkmanager "--licenses" && \
    sdkmanager "--update" && \
    sdkmanager "platform-tools" \
    "extras;android;m2repository" \
    "extras;google;m2repository"

RUN yes | sdkmanager "build-tools;${BUILD_TOOLS}" \
    "platforms;android-${TARGET_SDK}" && \
    rm -rf /tmp/PackageOperation*