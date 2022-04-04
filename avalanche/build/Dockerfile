FROM golang:1.17.4-buster AS builder

RUN apt-get update && apt-get install -y --no-install-recommends bash=5.0-4 git=1:2.20.1-2+deb10u3 make=4.2.1-1.2 gcc=4:8.3.0-1 musl-dev=1.1.21-2 ca-certificates=20200601~deb10u2 linux-headers-amd64

WORKDIR /
RUN git clone https://github.com/ava-labs/avalanchego
WORKDIR  avalanchego
RUN ./scripts/build.sh /avalanchego/build/

WORKDIR /
RUN git clone https://github.com/DefiKingdoms/subnet-evm
WORKDIR subnet-evm
RUN ./scripts/build.sh /avalanchego/build/plugins/mDV3QWRXfwgKUWb9sggkv4vQxAQR4y2CyKrt5pLZ5SzQ7EHBv

FROM debian:11-slim AS execution

RUN mkdir -p /avalanchego/build
WORKDIR /avalanchego/build

COPY --from=builder /avalanchego/build/ .

EXPOSE 9650/tcp 9651/tcp 9651/udp
CMD [ "./avalanchego" ]
