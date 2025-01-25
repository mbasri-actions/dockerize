# Dockerize Action

This GitHub Action automates the process of building, pushing, and signing Docker images. It is designed to work with GitHub Container Registry and supports multi-platform builds.

## Features

- Build Docker images using `docker/build-push-action`
- Push Docker images to GitHub Container Registry
- Sign Docker images using `cosign`
- Supports multi-platform builds
- Caching for faster builds

## Inputs

| Name          | Description                                                                               | Default       |
|---------------|-------------------------------------------------------------------------------------------|---------------|
| `image_name`  | The name of the Docker image to build and push                                            | `null`    |
| `platform`    | The target platforms for the Docker image (available value: 'linux/amd64', 'linux/arm64') | `linux/amd64` |

## Outputs

| Name          | Description                                      |
|---------------|--------------------------------------------------|
| `digest`      | The digest of the pushed Docker image            |

## Usage

Here's an example of how to use this action in a GitHub Actions workflow:

```yaml
name: Build, Push and Sign Docker Image

on:
  push:
    branches: [ main, dev ]
  pull_request:
    branches: [ main ]
  workflow_dispatch:

jobs:
  build-and-sign:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@main
      - name: build-push-sign-docker
        uses: mbasri-actions/dockerize@main
        with:
          docker_directory: '.'
          image_name: 'my-image'
```

## Author

* [**Mohamed BASRI**](https://github.com/mbasri)

## License

This is free and unencumbered software released into the public domain. See the [LICENSE](./LICENSE) file for details.
