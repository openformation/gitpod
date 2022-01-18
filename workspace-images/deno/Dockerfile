FROM openformation/gitpod-base

LABEL authors="André König <andre.koenig@openformation.io>"

#
# Version Configuration
#
ARG DENO_VERSION=1.17.3
ARG DENO_RELEASE_URL=https://github.com/denoland/deno/releases/download/v$DENO_VERSION/deno-x86_64-unknown-linux-gnu.zip
ARG DENO_INSTALL_DIR=/home/gitpod/.deno

WORKDIR /home/gitpod

RUN sudo apt update && sudo apt install -yq unzip

RUN mkdir -p .deno/bin && \
  curl --fail --location --progress-bar --output "$DENO_INSTALL_DIR/bin/deno.zip" "$DENO_RELEASE_URL" && \
  unzip -d "$DENO_INSTALL_DIR/bin" -o "$DENO_INSTALL_DIR/bin/deno.zip" && \
  chmod +x "$DENO_INSTALL_DIR/bin/deno" && \
  rm "$DENO_INSTALL_DIR/bin/deno.zip"


RUN echo "export DENO_INSTALL=\"$DENO_INSTALL_DIR\"" >> .bashrc.d/deno
RUN echo "export PATH=$DENO_INSTALL_DIR/bin:$PATH" >> .bashrc.d/deno