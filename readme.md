# Open Formation 💚 Gitpod

This repository contains all configurations around our Gitpod workspaces.

- `workspace-images`: This directory contains all our base fine-tuned workspace images we're utilizing within our projects.

## Contribute

All the built container images are public, so please make sure not to expose anything sensitive within the respective Dockerfiles. If you need a secret within the container, make sure to utilize [Gitpod Variables](https://www.gitpod.io/docs/environment-variables) for that.

Whenever changes are getting merged into the `main` branch, the respective images will be build and pushed to [Docker Hub](https://hub.docker.com/). Afterwards, they are live for all engineers within the company.

## Copyright

Copyright © 2020 – 2022 Open Formation GmbH / Hamburg, Germany

All rights reserved.