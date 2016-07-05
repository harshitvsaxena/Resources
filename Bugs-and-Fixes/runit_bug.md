<a id="top"></a>

# Bugs and Fixes

[Main Page](README.md)

## runit Bug

When installing `git-all` this start to giving error while installing any package. It was also showing up while restarting the system.

```sh
sudo apt-get install runit
```

This is a bug mentioned in `https://bugs.launchpad.net/ubuntu` for various vesions of Ubnutu. Maybe the Ubuntu team has not get the chance to fix this.


The error was solved by the comment from `https://launchpad.net/~tony-vandenhaag`.

You can see his comment at this location: `https://bugs.launchpad.net/ubuntu/+source/runit/+bug/1448164/comments/15`

The simple workaround mentioned by the above guy is:

```sh
sudo apt-get update
sudo rm /sbin/start
sudo apt-get install runit
sudo ln -s /sbin/initctl /sbin/initctl
sudo apt-get update
sudo apt-get upgrade
```

The command `sudo ln -s /sbin/initctl /sbin/initctl` might give an error such as `ln: failed to create /sbin/initctl as it already exists`. This is okay and you can proceed.

Now you can again try this:
```sh
sudo apt-get install git-all
```

It will work.

[Main Page](README.md) | [Top](#top)

---

## The End
