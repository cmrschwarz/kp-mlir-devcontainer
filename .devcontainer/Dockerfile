FROM debian:12

SHELL ["/bin/bash", "-c"]

# install system dependencies
RUN apt-get update
RUN apt-get install -y \
    curl unzip zip git vim gdb valgrind \
    clang-14 lld-14 ccache cmake ninja-build \
    python3-dev python3-numpy pybind11-dev \
    gpg bash-completion clangd clang-format

# make sure clang is on the path
ENV PATH="$PATH:/usr/lib/llvm-14/bin/"

# setup user dir
RUN mkdir -p /home/student
WORKDIR /home/student

# setup user
RUN useradd -u 1000 student -s /bin/bash \
    && chown -R student:student /home/student
USER student
COPY bash_profile.sh /home/student/.bash_profile

# install sdkman
ENV sdkman_auto_answer=true
RUN curl -s "https://get.sdkman.io" | bash

# install scala
RUN source "/home/student/.sdkman/bin/sdkman-init.sh" \
    && sdk i scala 3.2.1 \
    && sdk i sbt \
    && sdk i java 22.3.r19-grl \
    && gu install native-image

# install just
RUN curl --proto '=https' --tlsv1.2 -sSf https://just.systems/install.sh \
    | bash -s -- --to "/home/student/just"
ENV PATH="$PATH:/home/student/just"

# checkout llvm
RUN git clone --single-branch --depth 1 \
    --branch llvmorg-17.0.6 https://github.com/llvm/llvm-project.git

# build llvm
COPY llvm-justfile /home/student/llvm-project/justfile
WORKDIR /home/student/llvm-project
RUN source /home/student/.bash_profile && \
    just cmake && \
    just build

# create workspace folder
RUN mkdir -p /home/student/kp-mlir
WORKDIR /home/student/kp-mlir


