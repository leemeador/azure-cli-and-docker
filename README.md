# azure-cli-and-docker

Creates a docker image based on 'golang' with docker and the azure cli installed inside. Designed to run as a non-root user inside the
container, in particular, the same user as does the 'docker run' so some folders belonging to that user can be
available inside the container (use -v /opt/myfolder:/opt/myfolder to make them available inside when /opt/myfolder is owned by that user)

It is assumed there is a docker group outside the container and the non-root user belongs to that group. So when that user does
'docker run' there is no sudo required.

When running this image be sure to include the following so the docker socket on the outside is available for running docker
 from inside:

``` bash
DOCKER_GID=$(stat -c '%g' /var/run/docker.sock)
USER_UID=$(id -u)
docker run -u $USER_UID:$USER_UID --group-add $DOCKER_GID \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -ti <this image name>
```
