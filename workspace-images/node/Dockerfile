FROM openformation/gitpod-base

LABEL authors="André König <andre.koenig@openformation.io>"

WORKDIR /home/gitpod

RUN sudo apt update && \
  sudo apt install -yq unzip && \
  curl -fsSL https://fnm.vercel.app/install | bash -s -- --install-dir "./.fnm" --skip-shell && \
  #
  # Install latest Node.js LTS release
  #
  .fnm/fnm env --shell bash --use-on-cd >> .bashrc.d/fnm && \
  echo "export PATH=$PATH:/home/gitpod/.fnm/" >> .bashrc.d/fnm && \
  echo 'eval "$(fnm env)"' >> .bashrc.d/fnm && \
  echo "fnm install --lts &> /dev/null" >> .bashrc.d/fnm && \
  echo "corepack enable" >> .bashrc.d/fnm
