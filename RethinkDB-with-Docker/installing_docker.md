<a id="top"></a>
# RethinkDB with Docker

[Main Page](README.md)

## Installing Docker

Installing Docker is pretty easy. You can just follow the steps needed mentioned here:
https://docs.docker.com/engine/installation/linux/

Please select your version of linux from the above mentioned link and follow through the tutorial there.

Here I've shown it for Ubuntu Xenial 16.04 LTS

---

#### Note:

Docker requires a 64-bit installation regardless of your Ubuntu version. Additionally, your kernel must be 3.10 at minimum. The latest 3.10 minor version or a newer maintained version are also acceptable.

## Steps to follow:

- Check your kernel version:

```sh
uname -r
```

- Update your apt resources, also ensure that APT works with the https method, and that CA certificates are installed.

```sh
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates
```

- Add the new GPG key. Check for this online at https://docs.docker.com/engine/installation/linux/ubuntulinux/

```sh
sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
```

- Open the `/etc/apt/sources.list.d/docker.list` file. If the file doesn’t exist, create it.

```sh
sudo vim /etc/apt/sources.list.d/docker.list
```

- Remove any existing entries in the above file. Add an entry for your Ubuntu operating system. I've added it for Ubuntu Xenial 16.04 [LTS]. Please check for yours at the link mentioned in above points.

```sh
deb https://apt.dockerproject.org/repo ubuntu-xenial main
```

Close and save your file by pressing `esc` key and entering `:wq` or `:x` and hiting `Enter` key.

- For Ubuntu Trusty, Wily, and Xenial, it’s recommended to install the linux-image-extra kernel package.

```sh
sudo apt-get update
sudo apt-get install linux-image-extra-$(uname -r)
```

- Installing Docker

```sh
$ sudo apt-get update
$ sudo apt-get install docker-engine
```
- Start Docker

```sh
sudo service docker start
```
- Verify docker is installed correctly.

```sh
sudo docker run hello-world
```

This command downloads a test image and runs it in a container. When the container runs, it prints an informational message. Then, it exits.

---

Disclaimer: Most of the part of this is taken from the link https://docs.docker.com/engine/installation/linux/ubuntulinux/. Please check this link for more info.

[Main Page](README.md) | [Top](#top)

---

## The End
