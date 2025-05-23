# SPDX-License-Identifier: MPL-2.0

FROM ubuntu:24.04

# Base setup
RUN apt-get update && apt-get install -y --no-install-recommends \
    bash \
    curl \
    libjson-c5 \
    libwebsockets19t64 \
    ca-certificates \
    libssl3 \
    pkg-config \
    procps \
    tmux \
    vim \
    emacs \
    nano \
    git \
    file \
    supervisor \
    libsigsegv-dev \
    libtool \
    gawk \
    libsigsegv2 \
    bison \
    flex \
    texinfo \
    zip \
    unzip \
    libffi-dev \
    autoconf \
    automake \
    libltdl-dev \
    make \
    libc-bin \
    locales \
    libiconv-hook-dev \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install ttyd (arch-aware)
RUN set -eux; \
    ARCH=$(uname -m); \
    case "$ARCH" in \
        x86_64)   BINARY="ttyd.x86_64" ;; \
        aarch64)  BINARY="ttyd.aarch64" ;; \
        armv7l)   BINARY="ttyd.armhf" ;; \
        armv6l)   BINARY="ttyd.arm" ;; \
        i686)     BINARY="ttyd.i686" ;; \
        *)        echo "Unsupported architecture: $ARCH" >&2; exit 1 ;; \
    esac; \
    curl -L "https://github.com/tsl0922/ttyd/releases/download/1.7.7/${BINARY}" -o /usr/local/bin/ttyd; \
    chmod +x /usr/local/bin/ttyd

# Install Vector
RUN curl --proto '=https' --tlsv1.2 -sSfL https://sh.vector.dev | bash -s -- -y --prefix /usr/local

WORKDIR /usr/src

RUN git clone https://git.savannah.gnu.org/git/smalltalk.git

WORKDIR /usr/src/smalltalk

RUN autoreconf --install --force
RUN ./configure --prefix=/opt/smalltalk
# Serialize make step as it tends to fail on arm64 otherwise
RUN make -j1
RUN make install

ENV PATH="/opt/smalltalk/bin:$PATH"

WORKDIR /usr/src

RUN git clone https://github.com/timfel/JSON-st

RUN gst-package JSON-st/package.xml

# Create dev user and working directory
RUN useradd -ms /bin/bash devuser
WORKDIR /home/devuser/app
RUN chown devuser:devuser /home/devuser/app

RUN mkdir -p \
        /var/log \
        /var/lib/vector \
        /var/log/vector \
        /var/run \
        /home/devuser/run && \
    chown -R devuser:devuser \
        /var/log \
        /var/lib/vector \
        /var/log/vector \
        /var/run \
        /home/devuser/run

# Vector config
COPY --chown=devuser:devuser vector.toml /etc/vector/vector.toml

# Supervisord config
COPY --chown=devuser:devuser supervisord.conf /etc/supervisor/conf.d/rawpair.conf

# TTYD wrapper script
COPY ttyd-wrapper.sh /usr/local/bin/ttyd-wrapper.sh
RUN chmod +x /usr/local/bin/ttyd-wrapper.sh

# .bashrc tweaks to trap exits
RUN echo 'trap "" EXIT' >> /home/devuser/.bashrc && \
    echo 'alias exit="echo Nope."' >> /home/devuser/.bashrc && \
    chown devuser:devuser /home/devuser/.bashrc && \
    chmod 0444 /home/devuser/.bashrc

# Environment
ENV TERM=xterm \
    LOG_USER_ID=devuser \
    LOG_WORKSPACE_ID=default \
    LOG_SESSION_ID=dev-session

USER devuser
EXPOSE 7681

CMD ["supervisord", "-c", "/etc/supervisor/conf.d/rawpair.conf"]
