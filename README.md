# azure-cli-and-docker

Creates a docker image based on 'golang' with docker and the azure cli installed

When running this image be sure to include:

``` bash
docker run -v /var/run/docker.sock:/var/run/docker.sock -ti <this image name>
```
