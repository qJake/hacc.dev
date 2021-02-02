---
layout: tocpage
title: Installation
subtitle: Get yourself up and running!
---

## Supervisor Addon

At this time, HACC cannot run as a supervisor addon.

Anyone who is on an older version that is still running as an addon, should consider upgrading to a standalone Docker installation. To do this, simply export your configuration, remove the addon, create a Docker container (instructions below), and import the same configuration.

## Docker Container

<img src="/img/docker-logo.png" height="48" alt="Docker Logo" />

HACC is published as a Docker container with a number of tags for various OSes and architectures.

**Image name: [qjake/hacc](https://hub.docker.com/r/qjake/hacc/tags){:target="_blank"}{:rel="nofollow"}**

The default (`latest`) tag will pull the most recent version running on *Debian (Buster Slim)* (AMD64 / x86-64).

### New to Docker?

Docker is a *container platform*. This means, in simple terms, that small virtual servers can run on your computer in the background and do cool things... like install and run HACC!

If you would like to learn about Docker basics, **[check out this introduction](https://docker-curriculum.com/#introduction){:target="_blank"}{:rel="nofollow"}**.

### Container Tags

| Tag                                                             | OS                   | Architecture  |
|-----------------------------------------------------------------|----------------------|---------------|
| `qjake/hacc:latest`<br />`qjake/hacc:latest-linux-debian-amd64` | Debian (Buster Slim) | amd64         |
| `qjake/hacc:latest-linux-ubuntu-amd64`                          | Ubuntu (Bionic)      | amd64         |
| `qjake/hacc:latest-linux-alpine-amd64`                          | Alpine (3.10)        | amd64         |

### Running HACC

Pull the container image:

    docker pull qjake/hacc

Next, run the container:

    docker run --name hacc -p 8095:8095 -v haccdata:/app/data qjake/hacc

#### Argument Breakdown

**`--name hacc`** names the container "HACC" which allows you to easily call `docker stop hacc` and `docker start hacc` to stop and start the container using this name.

**`-p 8095:8095`** maps the app's default web port 8095 to the same "external" port on the computer where Docker is running. If you want to change the outside port, for example if you want to run HACC on port 80, change the first port, e.g. `-p 80:8095`

**`-v haccdata:/app/data`** persists HACC's configuration and settings to a *docker volume* called "haccdata". If you would like to store your HACC configuration somewhere else, you can change the path on the left, for example:

* Linux: `-v /home/username/hacc:/app/data`
* Windows: `-v //c/users/[username]/hacc:/app/data`

**`qjake/hacc`** This is the image's tag you want to run. This can be as simple as `qjake/hacc`, or a specific OS like `qjake/hacc:latest-linux-alpine-amd64`. It's up to you!

#### Optional Arguments

**`--restart always`** - Add this to have the container always restart if it is stopped, except if it is stopped manually. [Refer to the Docker documentation on restart policies.](https://docs.docker.com/config/containers/start-containers-automatically/)

### Updating HACC

As long as you have persisted your config volume using the `-v` parameter, your configuration should persist while upgrading.

Still, on the admin homepage, you can press **Export Configuration** to save a copy of your config just in case.

To update HACC, you need to stop **and remove** the container, update the image, and re-run it.

Assuming you named your container `hacc` from above, simply run:

    docker stop hacc
    docker rm hacc
    docker pull qjake/hacc
    [your previous docker run command, e.g.] docker run --name hacc -p 8095:8095 -v haccdata:/app/data qjake/hacc

You should now be on the latest version!

### Removing HACC

You want to delete HACC? Really? <span class="emj">☹</span> Okay.

Stop your container, remove it, and remove the docker volume associated with it:

    docker stop hacc
    docker rm hacc
    docker volume rm haccdata

And if you don't even want the image in your image store:

    docker image rm qjake/hacc

Poof! It's gone. Sorry to see you go!

## Other Webserver

HACC is based on ASP.NET Core 3.1, and thus, can run in any environment that ASP.NET Core supports, including IIS, Linux (standalong and nginx), and more.

Note that you may need to build the project yourself if you want to use your own webserver. With IIS, for example, you can open the project in Visual Studio, right-click the project, and select Publish &gt; IIS Website.

For more information, refer to the Microsoft documentation for ASP.NET Core:

* [Host ASP.NET Core on Linux with Nginx](https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/linux-nginx?view=aspnetcore-3.1)