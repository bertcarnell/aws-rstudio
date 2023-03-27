# aws-rstudio

To develop aws rstudio images for production

## `awslinux` image

docker build -t aws-rstudio-1-system aws-rstudio-1-system
docker build -t aws-rstudio-2-rstudio aws-rstudio-2-rstudio
docker build -t aws-rstudio-3-java aws-rstudio-3-java
docker build -t aws-rstudio-4-r aws-rstudio-4-r
docker build -t aws-rstudio aws-rstudio-5-rpackages

## `ubuntu` image



To start a container:

```
docker run --rm -ti --security-opt seccomp=unconfined wch1/r-debug

# Then you can run R-devel with:
RD

# Or, to run one of the other builds:
RDvalgrind -d valgrind
RDsan
RDcsan
RDstrictbarrier
RDthreadcheck
```

The `--security-opt seccomp=unconfined` is needed to use `gdb` in the container. Without it, you'll see a message like `warning: Error disabling address space randomization: Operation not permitted`, and R will fail to start in the debugger.


To mount a local directory in the docker container:

```
docker run --rm -ti --security-opt seccomp=unconfined -v /my/local/dir:/mydir wch1/r-debug

# Mount the current host directory at /mydir
docker run --rm -ti --security-opt seccomp=unconfined -v $(pwd):/mydir wch1/r-debug
```


If you want to have multiple terminals in the same container, start the container with `--name` and use `docker exec` from another terminal:

```
# Start container
docker run --rm -ti --name rd --security-opt seccomp=unconfined wch1/r-debug

# In another terminal, get a bash prompt in the container
docker exec -ti rd /bin/bash
```

