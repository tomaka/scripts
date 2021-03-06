FROM ubuntu:trusty
MAINTAINER Parity Technologies <devops@parity.io>
WORKDIR /build

# install tools and dependencies
RUN apt-get -y update && \
        apt-get install -y --force-yes --no-install-recommends \
	software-properties-common \
        curl \
        git \
        file \
        binutils \
	binutils-dev \
	make \
	ca-certificates \
	g++ \
	zip \
	dpkg-dev \
	python \
	rhash \
	openssl \
	build-essential \
	pkg-config \
	libssl-dev \
	libudev-dev 

# install java8
RUN add-apt-repository -y ppa:webupd8team/java
RUN apt-get update
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
RUN apt-get install -y oracle-java8-installer

# install nodejs
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get install -y nodejs && \
    apt-get clean

# install AWS CLI
RUN curl -O https://bootstrap.pypa.io/get-pip.py && \
    python get-pip.py && \
    pip install awscli

# cmake and llvm ppas. then update ppas
RUN add-apt-repository -y "ppa:george-edison55/cmake-3.x" && \
        add-apt-repository "deb http://llvm.org/apt/trusty/ llvm-toolchain-trusty-3.7 main" && \
        apt-get update && \
        apt-get install -y --force-yes cmake llvm-3.7-dev

# install rustup
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y

# rustup directory
ENV PATH /root/.cargo/bin:$PATH

# setup rust beta and nightly channel's
RUN rustup install beta
RUN rustup install nightly

# setup default stable channel
RUN rustup default stable

#rustup show
RUN rustup show

# show backtraces
ENV RUST_BACKTRACE 1

# Set default user
USER root


