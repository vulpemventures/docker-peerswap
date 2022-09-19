FROM golang:1.18-buster as builder

WORKDIR /app

ARG COMMIT=615d00b15790f0caffae4e4ebc7e6ac16665ccf2

RUN set -ex \
	&& git clone https://github.com/vulpemventures/peerswap && cd peerswap && git checkout ${COMMIT} \
	&& make -j$(nproc) build

FROM debian:buster-slim

# $USER name, and data $DIR to be used in the `final` image
ARG USER=peerswap
ARG DIR=/home/peerswap

# NOTE: Default GID == UID == 1000
RUN adduser --disabled-password \
            --home "$DIR/" \
            --gecos "" \
            "$USER"
USER $USER

COPY --from=builder /app/peerswap/out/* /usr/local/bin/


# Prevents `VOLUME $DIR/.peerswap/` being created as owned by `root`
RUN mkdir -p "$DIR/.peerswap/"

# Expose volume containing all `peerswapd` data
VOLUME $DIR/.peerswap/


ENTRYPOINT [ "peerswapd" ]


