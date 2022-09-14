# Docker PeerSwap

Dockerfile of the public image [ghcr.io/vulpemventures/peerswap:latest](https://github.com/orgs/vulpemventures/packages/container/package/peerswap)

Pull the image:

```bash
$ docker pull ghcr.io/vulpemventures/peerswap:latest
```

Run the image:

```bash
$ docker run -v path/to/peerswap.conf:/home/peerswap/.peerswap -d ghcr.io/vulpemventures/peerswap:latest
```

## Release

To tag a new image with a new version:

1) Create a new folder with `COMMIT` as directory name and change the `Dockerfile`s ARG `COMMIT`
2) Modify the GH Action in `.github/workflows/docker-publish.yml` changing the `COMMIT` env var
3) Push in master