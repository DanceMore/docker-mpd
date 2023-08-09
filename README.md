# docker-mpd

some of my workflows still depend on `mpd` and `randomcoww/mpd` is no longer availible for pulling, causing warnings in my logs.

instead of chasing down a new `mpd`, I decided to fork it, modernize it, and self-maintain it (mostly let CICD run)

pull via `ghcr.io` if you need it.

original readme below



### Docker MPD intended for HTTP streaming

https://hub.docker.com/r/randomcoww/mpd/

Default configuration creates a FLAC-3 stream over HTTP on port 8000

**Images**

https://hub.docker.com/repository/docker/randomcoww/mpd

#### Sample usage

```bash
podman run -it --rm \
    --security-opt label=disable \
    -v music_path:/mpd/music \
    -v cache_path:/mpd/cache \
    -p 6600:6600 \
    -p 8000:8000 \
    ghcr.io/randomcoww/mpd:0.23.5
```

### Image build

```
mkdir -p build
export TMPDIR=$(pwd)/build

VERSION=0.23
PATCH=5

podman build \
  --build-arg VERSION=$VERSION \
  --build-arg PATCH=$PATCH \
  -f Dockerfile \
  -t ghcr.io/randomcoww/mpd:$VERSION.$PATCH
```

```
podman push ghcr.io/randomcoww/mpd:$VERSION.$PATCH
```
