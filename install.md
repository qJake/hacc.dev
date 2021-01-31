---
layout: tocpage
title: Installation
subtitle: Get yourself up and running!
---

## Docker Container

<img src="/img/docker-logo.png" height="48" alt="Docker Logo" />

HACC is also published as a Docker container with a number of tags for various OSes and architectures.

**Image name: [qjake/hacc](https://hub.docker.com/r/qjake/hacc/tags){:target="_blank"}{:rel="nofollow"}**

The default (`latest`) tag will pull the most recent version running on *Debian (Buster Slim)* (AMD64 / x86-64).

### New to Docker?

If you are not familiar with Docker, it is highly recommended to use the Home Assistant Supervisor Add-on interface above. If you installed *Home Assistant Core* instead of the full *Home Assistant*, we recommend upgrading to the Supervisor-enabled version that has built-in support for add-ons.

If you would like to learn about Docker basics, **[check out this introduction](https://docker-curriculum.com/#introduction){:target="_blank"}{:rel="nofollow"}**.

### Container Tags

| Tag                                                             | OS                   | Architecture  |
|-----------------------------------------------------------------|----------------------|---------------|
| `qjake/hacc:latest`<br />`qjake/hacc:latest-linux-debian-amd64` | Debian (Buster Slim) | amd64         |
| `qjake/hacc:latest-linux-ubuntu-amd64`                          | Ubuntu (Bionic)      | amd64         |
| `qjake/hacc:latest-linux-alpine-amd64`                          | Alpine (3.10)        | amd64         |
| `qjake/hacc:latest-linux-debian-arm32v7`                        | Debian (Buster Slim) | arm32v7       |
| `qjake/hacc:latest-linux-debian-arm64v8`                        | Debian (Buster Slim) | arm64v8       |

### Running HACC

Pull the container image:

    docker pull qjake/hacc

Next, run the container:

    docker run --name hacc -p 8095:8095 -v haccdata:/app qjake/hacc

#### Argument Breakdown

**`--name hacc`** names the container "HACC" which allows you to easily call `docker stop hacc` and `docker start hacc` to stop and start the container using this name.

**`-p 8095:8095`** maps the app's default web port 8095 to the same "external" port on the computer where Docker is running. If you want to change the outside port, for example if you want to run HACC on port 80, change the first port, e.g. `-p 80:8095`

**`-v haccdata:/app`** persists HACC's configuration and settings to a *docker volume* called "haccdata". If you would like to store your HACC configuration somewhere else, you can change the path on the left, for example, on a Linux-based system, to store HACC's data in your home directory, use `-v /home/username/hacc:/app`.

**`qjake/hacc`** This is the image's tag you want to run. This can be as simple as `qjake/hacc`, or a specific OS like `qjake/hacc:latest-linux-alpine-amd64`. It's up to you!

### Updating HACC

As long as you have persisted your config volume using the `-v` parameter, your configuration should persist while upgrading.

Still, on the admin homepage, you can press **Export Configuration** to save a copy of your config just in case.

To update HACC, you need to stop the container, update the image, and restart it.

Assuming you named your container `hacc` from above, simply run:

    docker stop hacc
    docker pull qjake/hacc
    docker start hacc

You should now be on the latest version!

### Removing HACC

You want to delete HACC? Really? :( Okay.

Stop your container, remove it, and remove the docker volume associated with it:

    docker stop hacc
    docker rm hacc
    docker volume rm haccdata

And if you don't even want the image in your image store:

    docker image rm qjake/hacc

Poof! It's gone. Sorry to see you go!

## Other Webserver

HACC is based on ASP.NET Core 3.1, and thus, can run in any environment that ASP.NET Core supports, including IIS, Linux (standalong and nginx), and more.

For more information, refer to the Microsoft documentation for ASP.NET Core:

* [Host ASP.NET Core on Linux with Nginx](https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/linux-nginx?view=aspnetcore-3.1)