<a id="top"></a>

# RethinkDB with Docker

[Main Page](README.md)

## Setting Up RethinkDB

Pull rethinkDB like this:

```sh
$ sudo docker pull rethinkdb
```

Now use `run` command to start rethinkDB:

```sh
$ sudo docker run -d -P --name someName -v "$PWD:/data" rethinkdb
```

In the above command, `-d` will detach our terminal, `-P` will publish all exposed ports to random ports, `--name` corresponds to a name we want to give and finally `-v` is for bind mount a volume. All this you can refer from `docker run --help`.

Now, we can see the ports by running the `docker port [CONTAINER]` command

```sh
$ sudo docker port someName
28015/tcp -> 0.0.0.0:32769
29015/tcp -> 0.0.0.0:32768
8080/tcp -> 0.0.0.0:32770
```

Now open browser and see rethinkDB running at: http://localhost:32770

#### Some Important Commands:

To stop a container:
```sh
$ sudo docker stop [container ID without square brackets]
```

To restart a container:
```sh
$ sudo docker restart [container ID without square brackets]
```

To start a container:
```sh
$ sudo docker start [container ID without square brackets]
```

To send SIGKILL signal to the container:
```sh
$ sudo docker kill [container ID without square brackets]
```

You can get the container ids by using the command `docker ps -a`.

[Main Page](README.md) | [Top](#top)

---

## The End
