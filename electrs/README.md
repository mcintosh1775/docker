# Electrum Docker Build Process

In the current directory to build without any changes just do the following:

```
docker build .
docker tag 9738e2425919 amd64/electrs:v0.2
docker image ls
```
This image is based off Debian "Bookworm" docker image
