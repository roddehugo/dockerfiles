# To generate a new docker image with this dockerfile:
# $ docker build . -t multi-compilers:<tag>

FROM debian:buster
LABEL maintainer "Hugo Rodde <hugo.rodde@me.com>"

RUN apt-get update && apt-get -y upgrade

RUN apt-get -y install \
    software-properties-common \
    build-essential \
    tar bzip2 \
    git wget \
    python3 \
    libsdl2-dev

# Install Clang toolchain
RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key|apt-key add -
RUN apt-add-repository "deb http://apt.llvm.org/buster/ llvm-toolchain-buster main"
RUN apt-get update && apt-get -y install clang libclang-dev

# Install ARM GCC toolchain
RUN wget https://developer.arm.com/-/media/Files/downloads/gnu-rm/9-2020q2/gcc-arm-none-eabi-9-2020-q2-update-x86_64-linux.tar.bz2 \
    -O /tmp/gcc-arm-none-eabi-9-2020-q2-update-x86_64-linux.tar.bz2
RUN tar xvfj /tmp/gcc-arm-none-eabi-9-2020-q2-update-x86_64-linux.tar.bz2 -C /usr/local/
RUN rm /tmp/gcc-arm-none-eabi-9-2020-q2-update-x86_64-linux.tar.bz2
ENV PATH=$PATH:/usr/local/gcc-arm-none-eabi-9-2020-q2-update/bin

# Create a CI user
RUN adduser --disabled-password --gecos "CI" ci
USER ci
WORKDIR /home/ci
