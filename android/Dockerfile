Last login: Fri Jul  1 00:00:38 on ttys000
lizhaotailang@lizhaotngdeMini ~ % cd Downloads 
lizhaotailang@lizhaotngdeMini Downloads % ls
Dockerfile.uu
lizhaotailang@lizhaotngdeMini Downloads % vi Dockerfile.uu 



















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


