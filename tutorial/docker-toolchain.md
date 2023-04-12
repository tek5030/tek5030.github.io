[<-- Home](/)

# TEK 5030 - Getting started with Docker toolchain

This is a quick and dirty howto for getting started with the _Docker toolchain_ in CLion. YMMV!

### Prerequisites

- Have Docker installed and know how to use it.   
  https://docs.docker.com/engine/install/ubuntu/

- Familiarize yourself with _Docker toolchain_ in CLion, as described in the official documentation   
  https://www.jetbrains.com/help/clion/clion-toolchains-in-docker.html

- Pull the tek5030 docker image  

  ```bash
  docker pull tek5030/devcontainer:latest
  ```

### Setup the toolchain

- Create the toolchain as described in the [video].   
Use `tek5030/devcontainer:latest` as the Docker image.

- Create the Docker CMake configuration as described in the [video].

### Compile and run the labs

If you are working with a camera, like the RealSense-camera, the easiest way to run the lab is to do it from a terminal (it may very well be the internal terminal of CLion, if you please.

Here is what worked for the stereo lab:

```bash
docker run -it --rm \
    -v /dev:/dev \
    -v ${PWD}:/tmp/solution-stereo \
    -w /tmp/solution-stereo/cmake-build-release-docker \
    --device-cgroup-rule "c 81:* rmw" \
    --device-cgroup-rule "c 189:* rmw" \
    -e DISPLAY="${DISPLAY}" \
    -e XDG_RUNTIME_DIR="${XDG_RUNTIME_DIR}" \
    -v ${XDG_RUNTIME_DIR}:${XDG_RUNTIME_DIR} \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    tek5030/devcontainer:latest ./lab_7_stereo
```


---

[<-- Home](/)

[video]: https://www.jetbrains.com/help/clion/clion-toolchains-in-docker.html

