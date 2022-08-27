<!--
Maintainer:   jeffskinnerbox@yahoo.com / www.jeffskinnerbox.me
Version:      1.0.0
-->

# Snippet Box
Snippet Box is a simple, self-hosted app for organizing your code snippets.
It supports Markdown documentation for companion notes or simple documentation for your code.
It it makes it easily to create, edit, browse, and manage your snippets in various languages.
You'll find a Docker container for Snippet Box on DockerHub [pawelmalak/snippet-box][01].

Sources:

* [pawelmalak/snippet-box][01]
* [Snippet Box - Simple Code Snippet Management in Docker](https://www.youtube.com/watch?v=Y8OrPZADPkc)
* [Pi-Hosted: My Most used container! Snippet Box](https://www.youtube.com/watch?v=v-jUyB3fvAo)
* [How to install Snippet Box in Docker](https://smarthomepursuits.com/how-to-install-snippet-box-in-docker/)

## Pull from Github
Pulling this repository from GitHub gives you a quick and easy setup for Snippet Box.
You just need to set the environment variable in the scripts below for your environment.

```bash
# create a directory for snippet box
mkdir ~/src/snippet-box

# pull from github the required files for snippet box
cd ~/src/snippet-box
git pull https://github.com/jeffskinnerbox/snippet-box.git
```

## Install Snippet Box (on Linux)
I prefer to launch Snippet Box via `docker-compose`.
Install Snippet Box via `docker-compose` using the commandline:

```bash
# start the snippet-box docker container via docker-compose
sudo SNIPPET_PORT=5000 SNIPPET_DATA='./data' \
    docker-compose --file ./snippet-box-docker-compose.yml up -d
```

The Docker Compose file looks like this:

```yaml
version: '3'
services:
  snippet-box:
    container_name: snippet-box
    image: pawelmalak/snippet-box:latest
    volumes:
      - ${SNIPPET_DATA}:/app/data
    ports:
      - ${SNIPPET_PORT}:5000
    restart: unless-stopped
```

Installation of Snippet Box via the `docker` commandline,
you use the following:

```bash
# launch snippet box container via docker
sudo SNIPPET_PORT=5000 SNIPPET_DATA='./data' docker run -d \
    --name='snippet-box' \
    -p $(SNIPPET_PORT):5000
    -v $(SNIPPET_DATA):/app/data
    pawelmalak/snippet-box:latest
```

>**NOTE:** The Snippet Box GitHub also has a source code installation method documented [here][02].


-----


## Update Your Docker Container
You can update you Docker containers via the commandline,
but Portainer provides a intuitive browser UI to do the same.
Check out these videos:

* [Use Portainer to update your Docker Containers while they are running. No command line needed](https://www.youtube.com/watch?v=Eme2TlR7Z7E)
* [How to Update a Docker Container using Portainer](https://www.wundertech.net/how-to-update-a-docker-container-using-portainer/)

## Removing Snippet Box Images & Containers
If you run into problems, log into it or kill Snippet Box
and clean-up any unused resources
(i.e. images, containers, volumes, and networks)
that are dangling (not tagged or associated with a container).

How to do this is shown below:

```bash
# log into the snippet-box docker container and check out its operational status
sudo docker exec -it snippet-box bash

# kill the container
sudo docker kill snippet-box

# remove the container image
sudo docker rmi pawelmalak/snippet-box

# list any dangling images
sudo docker images -f dangling=true
```

This final step you **may not** want to perform.
It will delete the configuration and database record files you have created via Snippet Box.
At a minimum, you might want to create a copy of the data files.

```bash
# remove snippet's persistent data files
sudo rm -f -r data
```

Another clean up step you **may no** want to perform is of dangling and unreferenced
unused containers, networks, images.

```bash
# removes all unused containers, networks, images (both dangling and unreferenced), and optionally, volumes
sudo docker system prune
```

Source:

* [How To Remove Docker Images, Containers, and Volumes](https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes)



[01]:https://hub.docker.com/r/pawelmalak/snippet-box
[02]:https://github.com/pawelmalak/snippet-box/wiki/Installation-without-Docker
