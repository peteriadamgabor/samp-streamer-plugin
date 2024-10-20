FROM ubuntu:18.04

# Add i386 architecture and install required packages
RUN dpkg --add-architecture i386 && \
    apt-get update && \
    apt-get install -y \
        gpg \
        wget \
    && \
    wget -O- https://apt.kitware.com/keys/kitware-archive-latest.asc 2>/dev/null | \
    gpg --dearmor - | \
    tee /usr/share/keyrings/kitware-archive-keyring.gpg >/dev/null && \
    echo 'deb [signed-by=/usr/share/keyrings/kitware-archive-keyring.gpg] https://apt.kitware.com/ubuntu/ bionic main' | \
    tee /etc/apt/sources.list.d/kitware.list >/dev/null && \
    apt-get update && \
    apt-get install -y \
        cmake \
        ninja-build \
        g++-multilib \
        libstdc++6:i386 \
        libc6:i386 \
    && \
    useradd -m user

# Set user to 'user'
USER user

# Set environment variables for Latin-1 encoding
ENV LANG=es_ES.ISO-8859-1
ENV LC_ALL=es_ES.ISO-8859-1

# Update PATH variable
ENV PATH=~/.local/bin:${PATH}

# Copy the entrypoint script
COPY docker-entrypoint.sh /

# Set default command
CMD /docker-entrypoint.sh
