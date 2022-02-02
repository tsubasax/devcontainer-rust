FROM rust:1.58.1-slim-buster

ARG UID=1000
ARG GID=1000
ARG USER_NAME=vscode

# Change timezone
ENV TZ=Asia/Tokyo

# Install packages
RUN apt-get update \
  && apt-get -y install \
  git \
  locales \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Change locale
RUN sed -i -E 's/# (ja_JP.UTF-8)/\1/' /etc/locale.gen \
  && locale-gen ja_JP.UTF-8

ENV LANG=ja_JP.UTF-8
ENV LANGUAGE=ja_JP:ja
ENV LC_ALL=ja_JP.UTF-8

# Switch to non-root user
RUN groupadd -g "${GID}" "${USER_NAME}" \
  && useradd -lm -s /bin/bash -u "${UID}" -g "${USER_NAME}" "${USER_NAME}"

USER ${USER_NAME}

# Install Rust components
RUN rustup component add \
  clippy \
  rls \
  rustfmt \
  rust-analysis \
  rust-docs \
  rust-src

# Create workspace
WORKDIR /app