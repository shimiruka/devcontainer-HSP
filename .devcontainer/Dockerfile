# [Choice] Debian OS version (use bookworm, or bullseye on local arm64/Apple Silicon): bookworm, buster, bullseye
ARG VARIANT="bookworm"
FROM debian:${VARIANT}

# Install needed packages. Use a separate RUN statement to add your own dependencies.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get install -y --no-install-recommends \
    g++ make \
    fonts-noto-cjk \
    libgtk2.0-dev \
    libglew-dev \
    libsdl2-dev libsdl2-image-dev libsdl2-mixer-dev libsdl2-ttf-dev\
    libgles2-mesa-dev libegl1-mesa-dev \
    libcurl4-openssl-dev \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Clone OpenHSP repository and build it.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get install -y --no-install-recommends git ca-certificates \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/* \
    && git clone https://github.com/onitama/OpenHSP \
    && apt-get purge -y git ca-certificates \
    && cd OpenHSP \
    && make

# Add settings to avoid Gtk-WARNING.
RUN mkdir -p /home/vscode/.local/share/ \
    && touch /home/vscode/.local/share/recently-used.xbel

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>
