FROM rust:1.75.0-slim-bookworm AS builder

ARG VERSION=v0.10.2
ENV REPO=https://github.com/romanz/electrs.git

WORKDIR /build

RUN apt-get update
RUN apt-get install -y git cargo clang cmake libsnappy-dev

# libc-bin=2.36-9+deb12u3

RUN git clone --branch $VERSION $REPO .

RUN cargo build --release --bin electrs


FROM debian:bookworm-slim

COPY --from=builder /build/target/release/electrs /bin/electrs

# Electrum RPC Mainnet
EXPOSE 50001

# Prometheus monitoring
EXPOSE 4224

STOPSIGNAL SIGINT

HEALTHCHECK CMD curl -fSs http://localhost:4224/ || exit 1

ENTRYPOINT [ "electrs" ]
