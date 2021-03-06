**Note**: this repository is archived as the Woodpecker project is now offering official ARM64 images.

# Multi-Arch Woodpecker Builds

This repo is set up to automate creating multi-arch Docker images (arm64, amd64) for
the [Woodpecker CI system](https://woodpecker.laszlo.cloud/), a free fork of [Drone](https://drone.io/).

As of 2022-01-28, this only builds the Woodpecker server as ARM64 and AMD64 images. This is because
the Woodpecker project now provides multi-arch agent images themselves, but the server continues to
be AMD64 only (as of now).

The submodule for Woodpecker is primarily here for future monitoring for updates via Dependabot;
the actual meat of this project is just the three Dockerfiles and the GitHub Actions workflow.

`Dockerfile.build` is a Dockerfile that will run Woodpecker's unit tests and build the server and agent
executables inside a Docker container, so that multi-arch builds can be created using `docker buildx`;
the `Dockerfile.agent` and `Dockerfile.server` files will then copy the executables out of the relevant
containers and into new Alpine Linux containers to minimise final image size.

The finished images are available as:
- [florianpiesche/woodpecker-server](https://hub.docker.com/r/florianpiesche/woodpecker-server)
- [ghcr.io/fpiesche/woodpecker-server](https://ghcr.io/fpiesche/woodpecker-server)

The `latest` tag is the most recent release build; the `dev` tag the most recent commit to the main
Woodpecker repository. Images for release builds are also tagged with the specific git release tag,
and development builds with the git commit ID they were built from.
