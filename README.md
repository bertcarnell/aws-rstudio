# aws-rstudio

To develop aws rstudio images for production

## `awslinux` image

```
docker build -t aws-rstudio-1-system aws-rstudio-1-system
docker build -t aws-rstudio-2-rstudio aws-rstudio-2-rstudio
docker build -t aws-rstudio-3-java aws-rstudio-3-java
docker build -t aws-rstudio-4-r aws-rstudio-4-r
docker build -t aws-rstudio aws-rstudio-5-rpackages
```

## `ubuntu` images

### `ubuntu-rstudio`

```
docker build --progress plain -t ubuntu-rstudio-1-system ubuntu-rstudio-1-system
docker build --progress plain -t ubuntu-rstudio-2-rstudio ubuntu-rstudio-2-rstudio
docker build --progress plain -t ubuntu-rstudio-3-java ubuntu-rstudio-3-java
docker build --progress plain -t ubuntu-rstudio-4-r ubuntu-rstudio-4-r
docker build --progress plain -t ubuntu-rstudio-5-rpackages ubuntu-rstudio-5-rpackages
docker build --progress plain -t ubuntu-rstudio ubuntu-rstudio-6-other
```

### `ubuntu-sms` Sagemaker Studio R kernel

```
docker build --progress plain -t ubuntu-sms-1 ubuntu-sms-1
docker build --progress plain -t ubuntu-sms-2 ubuntu-sms-2
docker build --progress plain -t ubuntu-sms-3 ubuntu-sms-3
docker build --progress plain -t ubuntu-sms-4 ubuntu-sms-4
docker build --progress plain -t ubuntu-sms-5 ubuntu-sms-5
docker build --progress plain -t ubuntu-sms-6 ubuntu-sms-6
docker build --progress plain -t ubuntu-sms-7 ubuntu-sms-7
```


## To start a container:

```
docker run --rm -ti ubuntu-rstudio
docker run --rm -ti aws-rstudio
docker run --rm -ti ubuntu-sms-r
```

To start bash instead of the startup script

```
docker run -it --rm --user root ubuntu-sms-7 start.sh bash
```

To start ipython:  https://jupyter-docker-stacks.readthedocs.io/en/latest/using/common.html#user-related-configurations

```
docker run -it --rm --user root ubuntu-sms-7 start.sh ipython
```

To mount a local directory in the docker container:

```
docker run --rm -ti -v /my/local/dir:/mydir ubuntu-rstudio
```

Rebuild a container

```
docker build --no-cache
```

List and remove images

```
docker images --all
docker rmi <id>
```

