FROM debian:bullseye

LABEL version="0.1"
LABEL maintainer="nogajun+github@gmail.com"
LABEL description="sotmjp2022 build environment"

RUN apt-get -y update && apt-get -y full-upgrade && \
    apt-get -y --no-install-recommends install locales sudo build-essential git lv ruby ruby-dev bundler zlib1g-dev && \
    apt-get -y autoremove && apt-get -y clean && rm -rf /var/lib/apt/lists/*

ARG UID=1000
ARG GID=1000
ARG USER_LOCALE=ja_JP.UTF-8
ARG GEM=/usr/local/gem

RUN sed -i -e "s/^# \(${USER_LOCALE}\)/\1/g" /etc/locale.gen && \
    echo "LANG=${USER_LOCALE}" > /etc/default/locale && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=${USER_LOCALE} && \
    groupadd -g ${GID} docker && \
    useradd -u ${UID} -g ${GID} -s /bin/bash -m docker && \
    gpasswd -a docker docker && \
    mkdir -p ${GEM} && \
    chown ${UID}:${GID} ${GEM}

ENV LANG ${USER_LOCALE}
ENV LANGUAGE ja
ENV GEM_HOME ${GEM}

USER ${UID}
