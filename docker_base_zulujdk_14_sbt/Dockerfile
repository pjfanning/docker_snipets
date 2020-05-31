FROM docker:latest
ENV LANG C.UTF-8

ENV JAVA_VERSION 14.0.1-zulu
ENV SCALA_VERSION 2.13.2
ENV SBT_VERSION 1.3.12

RUN apk add --update \
    python \
    python-dev \
    py-pip \
    build-base \
    postgresql-client \
    postgresql-dev \
    curl \
    wget \
    bash \
    jq \
    openssl \
    tar \
    gzip \
    zip \
    unzip \
  && rm -rf /var/cache/apk/*

WORKDIR /root

COPY build.sbt .

RUN pip install awscli
RUN curl -s "https://get.sdkman.io" | bash
RUN bash -c "source $HOME/.sdkman/bin/sdkman-init.sh && \
    yes | sdk install java $JAVA_VERSION && \
    yes | sdk install sbt $SBT_VERSION && \
    rm -rf $HOME/.sdkman/archives/* && \
    rm -rf $HOME/.sdkman/tmp/* && \
    sbt sbtVersion compile && rm build.sbt"
