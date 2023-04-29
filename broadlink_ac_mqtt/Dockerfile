ARG BUILD_FROM=ghcr.io/hassio-addons/base/armhf:10.0.0
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# set version label
ARG BUILD_DATE
ARG VERSION
ARG AC2MQTT_VERSION
LABEL build_version="Version:- ${VERSION} Build-date:- ${BUILD_DATE}"
LABEL maintainer="emosenkis"

# set python to use utf-8 rather than ascii
ENV PYTHONIOENCODING="UTF-8"

RUN \
 echo "**** install packages ****" && \
apk add --no-cache --virtual=build-dependencies \
    g++ \
    gcc \
    curl \
    make \
    python3-dev \
    curl \
    && \
 apk add --no-cache \
        python3 \
        py3-paho-mqtt \
        py3-yaml \
        py3-pip \
        py3-parser \
        jq && \
 echo "**** install pip packages ****" && \
 pip install --no-cache-dir -U pycrypto && \
 echo "**** Install app ****" && \
 mkdir -p /app/ac2mqtt && \
 echo "Created App folder in /app/ac2mqtt" && \
 AC2MQTT_RELEASE=$(curl -sX GET "https://api.github.com/repos/liaan/broadlink_ac_mqtt/releases/latest" \
 | jq -r '. | .tag_name'); \
 echo "Latest Release is ${AC2MQTT_RELEASE}" && \
 echo "Downloading Version ${AC2MQTT_RELEASE}" && \
 curl -o \
 /tmp/ac2mqtt.tar.gz -L \
    "https://github.com/liaan/broadlink_ac_mqtt/archive/${AC2MQTT_RELEASE}.tar.gz" && \
 echo "Downloaded successfully, extracting to /app/ac2mqtt" && \
 tar xf \
 /tmp/ac2mqtt.tar.gz -C \
    /app/ac2mqtt --strip-components=1 && \
 echo "Extrcted successfully" && \
 echo "**** Hard Coding versioning ****" && \
 echo "None" > /app/ac2mqtt/version.txt && \
 echo ${AC2MQTT_RELEASE} > /app/ac2mqtt/version.txt && \
 echo "**** cleanup ****" && \
 apk del --purge \
    build-dependencies && \
 rm -rf \
    /root/.cache \
    /tmp/*

# copy local files
COPY root/ /
