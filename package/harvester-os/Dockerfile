ARG BASE_OS_IMAGE
FROM ${BASE_OS_IMAGE}

ARG ARCH=amd64
RUN curl -sfL https://github.com/rancher/wharfie/releases/download/v0.6.5/wharfie-${ARCH}  -o /usr/bin/wharfie && chmod +x /usr/bin/wharfie

COPY files/ /
RUN chmod 0600 /system/oem/*

COPY harvester-release.yaml /etc/

RUN mkinitrd

RUN curl -o /usr/bin/rancherd -sfL "http://192.168.0.181:8000/rancherd-amd64" && chmod 0755 /usr/bin/rancherd

ARG HARVESTER_PRETTY_NAME
RUN sed -i "s/^PRETTY_NAME.*/PRETTY_NAME=\"$HARVESTER_PRETTY_NAME\"/g" /etc/os-release && \
    echo GRUB_ENTRY_NAME="\"$HARVESTER_PRETTY_NAME\"" >> /etc/os-release

