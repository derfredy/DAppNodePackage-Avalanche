FROM debian:buster-slim as binary

ENV UPSTREAM_VERSION v1.1.2

ENV DOWNLOAD_URL https://github.com/ava-labs/avalanchego/releases/download/$UPSTREAM_VERSION/avalanchego-linux-amd64-$UPSTREAM_VERSION.tar.gz

RUN DEBIAN_FRONTEND=noninteractive \
    apt update && apt install --assume-yes --no-install-recommends wget ca-certificates && \
    wget -q ${DOWNLOAD_URL} && \
    tar xzf avalanchego-linux-amd64-$UPSTREAM_VERSION.tar.gz && \
    mv avalanchego-$UPSTREAM_VERSION avalanchego

FROM debian:buster-slim

#Copy binaries from build stage
COPY --from=binary avalanchego /root/avalanchego

ENTRYPOINT [ "sh", "-c", "exec /root/avalanchego/avalanchego \
  --plugin-dir=/root/avalanchego/plugins\
  $EXTRA_OPTS" ]