---
title: "Installation"
date: "`r format(Sys.time(), '%d %B, %Y')`"
draft: false
weight: 1
---
## Deployment

This is a docker image that eases setting up MapGallery for organizations. This image is based on the official [nginx](https://hub.docker.com/_/nginx) image.  Simple pull the image from the docker hub.

```bash
$ docker pull baasgeo/mapgallery:tagname
```

Alternatively you can build the image locally

```bash
$ git clone https://github.com/baasgeo/docker-mapgallery.git
$ cd mapgallery-docker
$ docker build -t "baasgeo/mapgallery:tagname" .
```

### Quick start

Create a data folder on your host:

```bash
$ sudo mkdir /var/mapgallery/
```

then run the container:

```bash
$ docker run \
    --name=mapgallery \
    --publish=8080:8081 \
    --volume /var/mapgallery:/usr/share/nginx/assets \
    --memory 32mb \
    baasgeo/mapgallery:4
```

Point your browser to `http://localhost:8080/` and login using MapGallery's default username and password:

- Username: admin
- Password: admin

## How to use different versions

There is mainly one version tag of this image for every minor **MapGallery** version.

- 4.0.x -> baasgeo/mapgallery:4.0
- 4.1.x -> baasgeo/mapgallery:4.1
- 4.2.x -> baasgeo/mapgallery:4.2
- 5.0.x -> baasgeo/mapgallery:5.0

...and so on.  

Patches are applied to the minor version whenever an update of MapGallery is available. Simply update to the latest version by pulling the image again.

```bash
$ docker pull baasgeo/mapgallery:tagname
$ docker restart mapgallery
```

## Configuration

### Data volume

This MapGallery container keeps its configuration data at `/usr/share/nginx/assets` which is exposed as volume in the dockerfile.
The volume allows for stopping and starting new containers from the same image without losing all the data and custom configuration.

You may want to map this volume to a directory on the host. Volumes can be mounted by passing the `-v` or `--volume` flag to the docker run command:

```bash
--volume /var/mapgallery:/usr/share/nginx/assets
```
This will also ease the upgrade process in the future. 


### Resource constraints

By default, the container has no resource constraints and can use as much of a given resource as the host’s kernel scheduler allows. To control how much memory, or CPU a container can use, apply runtime configuration flags of the `docker run` command as described here: [Runtime options with Memory, CPUs, and GPUs](https://docs.docker.com/config/containers/resource_constraints/)

### Database

MapGallery uses the PostgREST api with PostgreSQL database

#### PostgREST container

To set up the [PostgREST](https://postgrest.org) container, use the the official [postgrest](https://registry.hub.docker.com/r/postgrest/postgrest) image:

```bash
$ docker run -d --name="postgrest" postgrest/postgrest
```

For further information see [Docker Hub](https://registry.hub.docker.com/r/postgrest/postgrest)

Now start the MapGallery instance by adding the `--link` option to the docker run command:

```bash
--link postgrest:postgrest
```

#### PostgreSQL container

If you want to use a [PostgreSQL](https://www.postgresql.org/) container, you can link it to this image. You're free to use any PostgreSQL container.
An example with the official [postgres](https://registry.hub.docker.com/_/postgres/) image:

```bash
$ docker run -d --name="postgis" postgres
```

For further information see [Docker Hub](https://registry.hub.docker.com/_/postgres/)

Now start the MapGallery instance by adding the `--link` option to the docker run command:

```bash
--link postgres:postgis
```