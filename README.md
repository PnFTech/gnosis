## About
This project's aim is simple: to leverage the existing open-source [platform as a service (PaaS)](https://en.wikipedia.org/wiki/Platform_as_a_service),
[flynn](https://github.com/flynn/flynn), and NVIDIA-specific docker tools for
GPU device/library automatic discovery and mounting, [nvidia-docker](https://github.com/NVIDIA/nvidia-docker), to build a PaaS for GPU-accelerated applications.

**tl;dr**: *It's a PaaS for Machine Learning!*

## Building
To build from source, simply clone the repository, `cd` into the repo, and
execute the make command as follows:
```
$ git clone "https://github.com/RagingTiger/gnosis" && \
  cd gnosis && \
  which docker && \
  make build
```
**NOTE:** *`docker` must be installed or the build process will not work.*

The build process uses docker to build a container with the correct **Go**
environment, and **CUDA** libraries for working with both **flynn** and
**nvidia-docker**. This keeps your local host machine clean, and allows for
the build process to be cross platform. *This containerized build environment
is then perfect for developers who want to modify the source code, and need
a build environment to develop in (see the [Developing]() section).*

## Developing
After building the initial *docker image*, the same image can be used to
develop your own code. One potentially simple way to do this, is to create
a `developer` directory, mount it into the `gnosis:build` docker image, and
execute the `docker run` command as follows:
```
$ mkdir developer
$ docker run -v developer:/go/developer -it gnosis:build bash
```
This will allow you to share persistent files between the host and docker
container: what ever files you create in `developer` will be available in
both the container and on the host. This way if you create code you want to be
used in the container, or create/edit code in the container you want to
persist outside the container, you can if it is located in the `developer`
directory.
