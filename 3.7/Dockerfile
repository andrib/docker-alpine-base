FROM alpine:3.7
LABEL maintainer="andrib"

ENV S6_OVERLAY_VERSION=v1.21.4.0

# root filesystem
COPY rootfs /

### Add Core Utils
RUN apk --no-cache upgrade && \
    apk --no-cache add \
        bash \
        curl \
        grep \
        less \
        logrotate \
        nano \
        sudo \
        tzdata \
        && \
    rm -rf /var/cache/apk/* && \
    rm -rf /etc/logrotate.d/acpid && \
    cp -R /usr/share/zoneinfo/Asia/Jakarta /etc/localtime && \
    echo 'Asia/Jakarta' > /etc/timezone


# s6 overlay
RUN apk-install bash file

ADD https://github.com/just-containers/s6-overlay/releases/download/${S6_OVERLAY_VERSION}/s6-overlay-amd64.tar.gz /tmp/
RUN gunzip -c /tmp/s6-overlay-amd64.tar.gz | tar -xf - -C / \
    && rm /tmp/s6-overlay-amd64.tar.gz



ENTRYPOINT ["/init"]
