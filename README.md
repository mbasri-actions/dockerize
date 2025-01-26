# Dockerize Action

This GitHub Action automates the process of building, pushing, and signing Docker images. It is designed to work with GitHub Container Registry and supports multi-platform builds.

## Features

- Build Docker images using `docker/build-push-action`
- Push Docker images to GitHub [Container Registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry)
- Sign Docker images using `cosign`
- Supports multi-platform builds
- Caching for faster builds

## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_sigstore_cosign_installer"></a> [sigstore/cosign-installer](https://github.com/sigstore/cosign-installer) | 3.7.0 |
| <a name="requirement_docker_setup_qemu_action"></a> [docker/setup-qemu-action](https://github.com/setup-qemu-action) | 3.3.0 |
| <a name="requirement_docker_setup_buildx_action"></a> [docker/setup-buildx-action](https://github.com/docker/setup-buildx-action) | 3.8.0 |
| <a name="requirement_docker_login_action"></a> [docker/login-action](#requirement_docker_login_action) | 3.3.0 |
| <a name="requirement_docker_metadata_action"></a> [docker/metadata-action](https://github.com/docker/login-action) | 5.6.1 |
| <a name="requirement_docker_build_push_action"></a> [docker/build-push-action](https://github.com/docker/build-push-action) | 6.13.0 |

## Inputs

| Name | Description | Required | Default |
| --- | --- | --- | --- |
| <a name="input_registry"></a> [registry](#input_registry) | The registry to push the Docker image to | true | `ghcr.io` |
| <a name="input_docker_directory"></a> [docker-directory](#input_docker_directory) | The directory containing the Dockerfile | true | `.` |
| <a name="input_image_name"></a> [image-name](#input_image_name) | The name of the Docker image | true | `null` |
| <a name="input_platform"></a> [platform](#input_platform) | The platform to build the Docker image for | true | `linux/amd64` |
| <a name="input_tags"></a> [tags](#input_tags) | The tags to apply to the Docker image | false | `null` |
| <a name="input_github_token"></a> [github-token](#input_github_token) | The GitHub Token for pushing and signing the Docker image | true | `null` |

## Outputs

No Outputs

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
        uses: actions/checkout@v4
      - name: build-push-sign-docker
        uses: mbasri-actions/dockerize@v1.0.0
        with:
          registry: ghcr.io
          github-token: 'abc123'
          docker-directory: '.'
          image-name: 'my-image'
          tags: |
            ghcr.io/my-image:dev
```

## Author

* [**Mohamed BASRI**](https://github.com/mbasri)

## License

This is free and unencumbered software released into the public domain. See the [LICENSE](./LICENSE) file for details.
