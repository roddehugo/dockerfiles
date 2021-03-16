# To generate a new docker image with this dockerfile:
# $ docker build . -t multi-compilers:<tag>

FROM debian:buster-slim
LABEL maintainer "Hugo Rodde <hugo.rodde@me.com>"

RUN apt-get update && apt-get install -y --no-install-recommends \
        software-properties-common gnupg2 \
        gcc g++ libc6-dev make cmake \
        tar wget bzip2 git python3 \
    && rm -rf /var/lib/apt/lists/*

# Install Clang toolchain
RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key|apt-key add - \
    && apt-add-repository "deb http://apt.llvm.org/buster/ llvm-toolchain-buster main" \
    && apt-get update && apt-get install -y --no-install-recommends \
        clang libclang-dev \
    && rm -rf /var/lib/apt/lists/*

# Install ARM GCC toolchain
RUN wget https://developer.arm.com/-/media/Files/downloads/gnu-rm/9-2020q2/gcc-arm-none-eabi-9-2020-q2-update-x86_64-linux.tar.bz2 \
        -O /tmp/gcc-arm-none-eabi-9-2020-q2-update-x86_64-linux.tar.bz2 \
    && tar xvfj /tmp/gcc-arm-none-eabi-9-2020-q2-update-x86_64-linux.tar.bz2 \
        -C /usr/local/ \
    && rm /tmp/gcc-arm-none-eabi-9-2020-q2-update-x86_64-linux.tar.bz2
ENV PATH=$PATH:/usr/local/gcc-arm-none-eabi-9-2020-q2-update/bin

# Create a CI user
RUN adduser --disabled-password --gecos "CI" ci
USER ci
WORKDIR /home/ci
