FROM rust:1.58.1-alpine

ARG UID=1000
ARG GID=1000
ARG USER_NAME=vscode

ENV TZ=Asia/Tokyo \
  LANG=ja_JP.UTF-8 \
  LANGUAGE=ja_JP:ja \
  LC_ALL=ja_JP.UTF-8 

RUN addgroup -S -g "${GID}" "${USER_NAME}" \
  && adduser -u "${UID}" -G "${USER_NAME}" -D "${USER_NAME}" \
  # Install packages
  && apk --update --no-cache add \
  git \
  openssh \
  tzdata \
  && cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
  && apk del tzdata \
  # Install Rust components
  && rustup component add \
  rls \
  clippy \
  rustfmt \
  rust-src \
  rust-docs \
  rust-analysis

USER vscode

WORKDIR /app