FROM docker.io/bitnami/minideb:buster
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV HOME="/" \
    OS_ARCH="amd64" \
    OS_FLAVOUR="debian-10" \
    OS_NAME="linux"

COPY prebuildfs /
# Install required system packages and dependencies
RUN install_packages ca-certificates curl gzip jq procps tar wget
RUN wget -nc -P /tmp/bitnami/pkg/cache/ https://downloads.bitnami.com/files/stacksmith/kubectl-1.20.9-0-linux-amd64-debian-10.tar.gz && \
    echo "3c156ebbc9eb120bc4c38739b8cd044c9739c0db10f8f7797fb333f9ebc2f351  /tmp/bitnami/pkg/cache/kubectl-1.20.9-0-linux-amd64-debian-10.tar.gz" | sha256sum -c - && \
    tar -zxf /tmp/bitnami/pkg/cache/kubectl-1.20.9-0-linux-amd64-debian-10.tar.gz -P --transform 's|^[^/]*/files|/opt/bitnami|' --wildcards '*/files' && \
    rm -rf /tmp/bitnami/pkg/cache/kubectl-1.20.9-0-linux-amd64-debian-10.tar.gz
RUN chmod g+rwX /opt/bitnami

ENV BITNAMI_APP_NAME="kubectl" \
    BITNAMI_IMAGE_VERSION="1.20.9-debian-10-r5" \
    PATH="/opt/bitnami/kubectl/bin:$PATH"

USER 1001
ENTRYPOINT [ "kubectl" ]
CMD [ "--help" ]
