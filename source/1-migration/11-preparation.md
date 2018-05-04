# Preparation

**Warning**: this section is mostly based on original Void Linux wiki page. I strongly recommend you to check the wiki source first: some things discussed here may be already obsolete at the time of you reading and I can't guarantee their relevance.

## Obtaining Void Image

All the official Void Linux live images are stored in official Void [repository](https://repo.voidlinux.eu/) here:

> [repo.voidlinux.eu/live/current](https://repo.voidlinux.eu/live/current/)

You have to choose one of universal ISO images for `x86_64` architecture (sometimes `x86_64` is referenced as `x64` or `amd64` despite it's for any CPU vendor, not only AMD). Such images have name like `void-live-x86_64-[date]-[flavour].iso` and only differs by pre-installed *flavour* (desktop environment). I personally recommend you to choose the minimal image without any of DE since you'll anyway have to download and update all the packages, even they're were pre-installed on image.

# Flashing Media

On this step you'll need the USB flash stick.

## Flashing on Microsoft® Windows®

*No description provided*.

## Flashing on Unix-like systems

If you're already have one of Unix-like system (masOS should be suitable, but I never actually worked on it), then you can use simple command-line utility named *dd*.

First you need to locate your USB stick: eject all the portable devices, then open terminal emulator and type `ls /dev/sd*`. This will print something like that:

```plain
user@pc:~$ ls /dev/sd*
/dev/sda /dev/sda1 /dev/sda2 /dev/sda3 /dev/sda4
/dev/sdb /dev/sdb1 /dev/sdb2
```

Insert USB stick and run `ls /dev/sd*` once more:

```plain
user@pc:~$ ls /dev/sd*
/dev/sda /dev/sda1 /dev/sda2 /dev/sda3 /dev/sda4
/dev/sdb /dev/sdb1 /dev/sdb2
/dev/sdc /dev/sdc1 /dev/sdc2
```

New SCSI device was added: all the `/dev/sdc*` entries are refering your USB stick (actual letter may differs). Now you need to run the *dd* on it. This will only work under root, so you need to substitute user at first (you can skip this step if you have *sudo* available in the system):

```plain
user@pc:~$ su
# Entering  password - characters are invisible
root@pc:/home/user#
```

Now, run the *dd*. On this step you'll **overwrite** and thus **erase** all the USB stick contents, so please do in with caution.

```plain
  root@pc:/home/user# dd                                        \
                        if=/dev/sdc                             \
                        of=/path/to/void-live-x86_64-[date].iso \
                        status=progress
```

*Note*: backshashes `\` here added for readability, you can just type all the command in one line instead.

Eject you USB stick when *dd* ends (shell will print new prompt) and you're almost ready to system installation!

# Boot Preparation

To install the Void, you should boot from flash stick at first. It shoud be easy on modern motherboards on which you can just use boot override option — bad news is that you have to find this option by yourself. There is no universal way to do that, so you'll probably need to google at first. Sometimes this procedure is discussed in your PC manual, or such option might be prompted while booting ("Press F12 to select boot device" like on my laptop e.g.)
