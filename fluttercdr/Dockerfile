FROM ubuntu:latest

# Create a non-root user

# Install dependencies
RUN apt-get update && \
    apt-get install -y curl git unzip xz-utils zip libglu1-mesa openjdk-11-jdk wget fonts-firacode && \
    apt-get install -y clang cmake ninja-build pkg-config sudo zsh libgtk-3-dev liblzma-dev vim && \
    apt-get install -y x11-apps libx11-dev libxcomposite-dev libxcursor-dev libxdamage-dev libxext-dev libxfixes-dev libxi-dev libxinerama-dev libxrandr-dev libxss-dev libxtst-dev && \
    rm -rf /var/lib/apt/lists/ &&  apt-get clean && \
    rm -rf /tmp/* /var/tmp/* && curl -fsSL https://code-server.dev/install.sh | sh && \
    groupadd -g 1000 fluttercoder && \
    # useradd --create-home -ms /bin/zsh fluttercoder && \ 
    # groupadd fluttercoder -g 1000 && \
    useradd -ms /bin/zsh  --create-home -u 1000 fluttercoder -g 1000 && \
    # chsh -s $(which zsh) fluttercoder && \
    echo 'fluttercoder ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers && \
    mkdir -p /home/fluttercoder/.local/share/code-server/User/workspace/tinder && \
    chown -R fluttercoder:fluttercoder /home/fluttercoder



# Set ownership of home directory to non-root user
# RUN useradd -m -s /bin/zsh fluttercoder
# RUN chmod -R u+rwx /home/fluttercoder && \
# Switch to non-root user and set working directory


USER fluttercoder
WORKDIR /home/fluttercoder

# Install Flutter SDK
RUN git clone https://github.com/flutter/flutter.git /home/fluttercoder/flutter && \
    mkdir -p /home/fluttercoder/Android/cmdline-tools/latest && \
    wget -q https://dl.google.com/android/repository/commandlinetools-linux-9477386_latest.zip && \
    unzip commandlinetools-linux-9477386_latest.zip -d /home/fluttercoder/Android/cmdline-tools && \
    mv /home/fluttercoder/Android/cmdline-tools/cmdline-tools/* /home/fluttercoder/Android/cmdline-tools/latest/ && \
    rm commandlinetools-linux-9477386_latest.zip && \
    rm -rf /home/fluttercoder/Android/cmdline-tools/cmdline-tools

ENV PATH $PATH:/home/fluttercoder/flutter/bin
ENV ANDROID_HOME /home/fluttercoder/Android
ENV PATH $ANDROID_HOME/cmdline-tools/latest/bin:$PATH
ENV PATH $PATH:$ANDROID_HOME/platform-tools
ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk-amd64
ENV PATH $PATH:$JAVA_HOME/bin
ENV DISPLAY $DISPLAY



# Install Flutter SDK
# ...--privileged

# Expose code-server port

# Set the entrypoint




# RUN sdkmanager --update
# Install Android SDK components
RUN yes | sdkmanager --licenses && \
    sdkmanager "platform-tools" "platforms;android-33" "build-tools;33.0.2" && \
    code-server --install-extension Equinusocio.vsc-material-theme --force && \
    code-server --install-extension PKief.material-icon-theme --force && \
    code-server --install-extension Dart-Code.flutter --force && \
    echo '{ \
    "editor.fontFamily": "Fira Code", \
    "editor.fontSize": 18, \
    "editor.fontLigatures": true, \
    "workbench.colorTheme": "Material Theme Darker High Contrast", \
    "workbench.iconTheme": "material-icon-theme", \
    "files.autoSave": "onFocusChange", \
    "dart.flutterSdkPath": "/home/fluttercoder/flutter", \
    "dart.sdkPath": "/home/fluttercoder/flutter/bin/cache/dart-sdk" \
    }' > /home/fluttercoder/.local/share/code-server/User/settings.json && \
    flutter doctor --verbose && sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"


# Expose code-server port
EXPOSE 8080
# EXPOSE 5000
# USER root
# Start code-server


# CMD ["code-server", "--bind-addr", "0.0.0.0:8080", "--auth", "none"]
# CMD ["code-server", "--bind-addr", "0.0.0.0:8080", "--auth", "none", "--user-data-dir", "/home/fluttercoder/.config", "/home/fluttercoder/.local/share/code-server/User/workspace/tinder"]
CMD ["code-server", "--bind-addr", "0.0.0.0:8080", "--auth", "none", "--user-data-dir", "/home/fluttercoder/.local/share/code-server", "/home/fluttercoder/.local/share/code-server/User/workspace/tinder"]

# CMD ["code-server", "--bind-addr", "0.0.0.0:8080", "--auth", "none", "/home/fluttercoder/.local/share/code-server/User/workspace/tinder"]
