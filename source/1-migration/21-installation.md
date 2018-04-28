# Installation

Once Void is booted up, it will show the MOTD welcome message that promts existing users:

| Login  | Password    |
| ------ | ----------- |
| `root` | `voidlinux` |
| `anon` | `voidlinux` |

Root user should be used in order to install the system. Note that password characters are completely invisible while typing.

If root is logged correctly, its login shell (Dash currently) will show the prompt:

```plain
#
```

Dash lacks of many traditional shell features — it's unable to move carret by left-right arrows (prints `^[[D` and `^[[C` instead). However, this shell will be enough to install the system and do some optional stuff.

## Optional Pre-install Steps

You might want to remove old EFI boot entries of previous operating systems (e.g. Windows) before nstallation. Run the `efibootmgr` with no options and you'll see some EFI technical info with list of entries:

```plain
[some of data useless for now...]
Boot0000* Windows Boot Manager
Boot0001* Ubuntu
Boot0010* UEFI Onboard LAN IPv4
Boot0011* UEFI Onboard LAN IPv6
[other vendor boot entries]
```

**Be careful**: you can see the vendor-installed entries, do not remove them!

Indicate the old OS' entries (like 0000 and 0001 in example above) and run the following command:

```sh
efibootmgr -b BOOT_NUMBER -B
```

In example above, one should run this command twice, for each of useless enties:

```sh
efibootmgr -b 0000 -B
efibootmgr -b 0001 -B
```

## Installation Steps

Void provides custom installation master script which makes installation process pretty easy. To start master, run `void-installer` command.
