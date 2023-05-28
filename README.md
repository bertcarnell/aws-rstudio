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
```


## To start a container:

```
docker run --rm -ti ubuntu-rstudio
```

To mount a local directory in the docker container:

```
docker run --rm -ti -v /my/local/dir:/mydir ubuntu-rstudio
```
