ARG BUILD_FROM=ghcr.io/hassio-addons/debian-base:7.5.1
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Setup base
# hadolint ignore=DL3003

ENV container docker
ENV LC_ALL C
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    systemd=252.30-1~deb12u2 \
    systemd-sysv=252.30-1~deb12u2 \
    sudo=1.9.13p3-1+deb12u1 \
    wget=1.21.3-1+b1 \
    nginx=1.22.1-9 \
    procps=2:4.0.2-3 \
    iproute2=6.1.0-3 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && rm -fr \
        /tmp/* \
        /var/cache/* \
        /var/lib/apt/lists/* \
        /var/log/*.log \
        /var/log/apt  \
    && rm -f /lib/systemd/system/multi-user.target.wants/* \
    /etc/systemd/system/*.wants/* \
    /lib/systemd/system/local-fs.target.wants/* \
    /lib/systemd/system/sockets.target.wants/*udev* \
    /lib/systemd/system/sockets.target.wants/*initctl* \
    /lib/systemd/system/basic.target.wants/* \
    /lib/systemd/system/anaconda.target.wants/* \
    /lib/systemd/system/plymouth* \
    /lib/systemd/system/systemd-update-utmp* \
    && curl -sL https://install.raspap.com | bash -s -- --yes --wireguard 1 --openvpn 1 --adblock 1 --rest 1

# Copy root filesystem
COPY rootfs /

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

VOLUME [ "/sys/fs/cgroup" ]

# Labels
LABEL \
    io.hass.name="Addon RASPAP base for ${BUILD_ARCH}" \
    io.hass.description="Home Assistant Community Add-on: ${BUILD_ARCH} RASPAP base image" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="base" \
    io.hass.version=${BUILD_VERSION} \
    io.hass.base.version=${BUILD_VERSION} \
    io.hass.base.name="raspap" \
    io.hass.base.image="hassioaddons/raspap-base" \
    maintainer="ZENNED <azenned@gmail.com>" \
    org.opencontainers.image.title="Addon RASPAP base for ${BUILD_ARCH}" \
    org.opencontainers.image.description="Home Assistant Community Add-on: ${BUILD_ARCH} RASPAP base image" \
    org.opencontainers.image.vendor="Home Assistant Community Add-ons" \
    org.opencontainers.image.authors="ZENNED <azenned@gmail.com>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://addons.community" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
