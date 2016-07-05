<a id="top"></a>

# RethinkDB with Docker

[Main Page](README.md)

## Playing with Docker

This guide is for getting used to Docker.

---

#### Step 1. Playing with BusyBox

Run this command in terminal:

```sh
$ sudo docker pull busybox
```

The `pull` command fetches the `busybox image` from the Docker registry and saves it to our system.

##### What is BusyBox?

The Swiss Army Knife of Embedded Linux. BusyBox combines tiny versions of many common UNIX utilities into a single small executable. It provides replacements for most of the utilities you usually find in GNU fileutils, shellutils, etc. The utilities in BusyBox generally have fewer options than their full-featured GNU cousins; however, the options that are included provide the expected functionality and behave very much like their GNU counterparts. BusyBox provides a fairly complete environment for any small or embedded system.

More on BusyBox:
- https://en.wikipedia.org/wiki/BusyBox
- https://hub.docker.com/_/busybox/

Use this command to see a list of all images on your system.

```sh
$ sudo docker images
```

Now let's run the Docker container based on this image.

```sh
$ sudo docker run busybox
```

Nothing happened! Behind the scenes, a lot of stuff happened. When you call run, the Docker client finds the image (busybox in this case), loads up the container and then runs a command in that container. When we run docker run busybox, we didn't provide a command, so the container booted up, ran an empty command and then exited.

Now try this:


```sh
$ sudo docker run busybox echo "hello from busybox"
hello from busybox
```

The `docker ps` command shows you all containers that are currently running.

```sh
$ sudo docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

Since no containers are running, we see a blank line. Now use this:

```sh
$ sudo docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
305297d7a235        busybox             "uptime"            11 minutes ago      Exited (0) 11 minutes ago                       distracted_goldstine
ff0a5c3750b9        busybox             "sh"                12 minutes ago      Exited (0) 12 minutes ago                       elated_ramanujan
```

So what we see above is a list of all containers that we ran.

To run more than just one command in a container:

```sh
$ sudo docker run -it busybox sh
/ # ls
bin   dev   etc   home  proc  root  sys   tmp   usr   var
/ # uptime
 05:45:21 up  5:58,  0 users,  load average: 0.00, 0.01, 0.04
```

Running the run command with the `-it` flags attaches us to an interactive tty in the container. Now we can run as many commands in the container as we want.

To exit the above container use `exit` commant in the tty container.

We can exit the container and then start it up again with the `docker run -it busybox sh` command.

To find out more about run, use `docker run --help` to see a list of all flags it supports.

We ran `docker run` multiple times and leaving stray containers will eat up disk space. Hence, as a rule of thumb, clean up containers once done with them. To do that, you can run the `docker rm` command. Just copy the container IDs from the command `docker ps -a` and paste them alongside the command.

```sh
$ sudo docker rm 305297d7a235 ff0a5c3750b9
305297d7a235
ff0a5c3750b9
```

If you have a bunch of containers to delete in one go, copy-pasting IDs can be tedious. In that case, you can simply run:

```sh
$ sudo docker rm $(sudo docker ps -a -q -f status=exited)
```

---

Disclaimer: Major part of this document is taken from http://prakhar.me/docker-curriculum/.

[Main Page](README.md) | [Top](#top)

---

## The End
