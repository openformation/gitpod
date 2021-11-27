FROM openformation/gitpod-base

LABEL authors="André König <andre.koenig@openformation.io>"

RUN sudo apt update && \
  sudo apt install -yq unzip && \
  curl -fsSL https://fnm.vercel.app/install | bash -s -- --install-dir "./.fnm" --skip-shell && \
  #
  # Install latest Node.js LTS release
  #
  /home/gitpod/.fnm/fnm env --shell bash --use-on-cd >> /home/gitpod/.bashrc && \
  echo "export PATH=$PATH:/home/gitpod/.fnm/" >> /home/gitpod/.bashrc && \
  echo 'eval "$(fnm env)"' >> /home/gitpod/.bashrc && \
  echo "fnm install --lts &> /dev/null" >> /home/gitpod/.bashrc
