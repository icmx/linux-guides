# Terms and Definitions

This section describes some basic terms oftenly used in Linux community.

## Linux and GNU

In most of cases, when someone says "Linux", he (or she) means to say "operating system distribution based on Linux kernel and some of GNU components". This is quite long term to pronounce or write, so it gets shortened to just "Linux".

Meanwhile, real meaning of word Linux is perfectly described in ["I'd just like to interject for a moment..."](https://www.google.com/search?q=i%27d+just+like+to+interject+for+a+moment) text which supposedly belongs to [Richard Stallman](https://en.wikipedia.org/wiki/Richard_Stallman):

> Linux is the kernel: the program in the system that allocates the machine’s resources to the other programs that you run. The kernel is an essential part of an operating system, but useless by itself; it can only function in the context of a complete operating system.

However, not many people actually work with Linux as a kernel (to maintain e.g.), so you'll almost never be misunderstood when referring to Linux as a distribution or operating system. These guides refers to Linux as an operating system distribution unless specified otherwise.

GNU, in its turn, is a wide set of different software, incliding e.g. GIMP graphical editor, GTK+ graphical interface elements, Bash shell, Wget downloader and many other [cool things](https://en.wikipedia.org/wiki/List_of_GNU_packages) developed and curated by GNU Foundation. That is, in most cases GNU/Linux distribution is almost the same as Linux distribution since most of Linux distributions in any way use some of GNU components (Bash at least).

## Linux Distribution

Set of different software, primarily including Linux (as kernel) and usually some of GNU tools, drivers, user applications and such. Combined together, they provide another variation of GNU/Linux operating system which is often called "Linux distribution" or just "distro".

Most of Linux distributions are made for general purpose (i.e., for daily home usage, like Fedora, Ubuntu or Arch Linux), and include the basic set of pre-configured applications like[Window manager, composite manager, file manager, internet browser, office suite, text editors, calculators and other software, mostly from the set of one of desktop environments.

Popular distributions usually provide different installation image types, some of them are listed below:

  - Live — means that this image is ready to use without installation. Live images are great if you just want to try a new system (or rescue an old one), but I personally do not recommend them for everyday use — located on USB sticks, they may damage flash memory by unusually frequent reading and writing after continuous usage.
  - Net (netinst, netboot etc) — indicate compact images (about 40-400 MB) with minimal software set on board. Such types of images are commonly used by advanced users for deep system customization — however, there are user-friendly network images which provide special installation wizards. I personally recommend you to use such images if you have stable internet connection with appropriate speed (≥ 500 Mbps will be enough).
  - Flavor — most of popular distributions provide multiple images with different pre-installed desktop environments on them. Images with primary DE usually have official status while other images are considered as optionals and called flavors.

Multiple types can be combined in one image, e.g. netboot image that provides XFCE desktop environment after installation.

## Unix, POSIX and Unix-like

**Unix** is an old (circa 1970) operating systems family, initially developed as closed source software and inspired by some of [Multics](https://www.multicians.org/) early operating system features and conceptions.

**POSIX** is a modern industrial standard, which mostly relies on Unix behaviour and features. It was developed to maintain compatibility between different Unix-like operating systems.

**Unix-like** system is an operating system that fulfills two conditions:

  1. It behaves like Unix systems, and
  2. (optionally) It is POSIX-certified

Most notable examples of Unix-like operating systems are macOS, FreeBSD and, of course, Linux (including Void). They're not POSIX-certified, but mostly works as POSIX specifications stands for.

## Command Line Interface (CLI)

Application interface in which user is supposed to type some textual commands. On Microsoft® Windows® systems you can press Win + R, type `cmd` or `powershell` and see the examples of CLI.

Command line interface is still considered as main user interface for most of Unix-like operating systems, including Linux. It might be hard to learn, but after a while it becomes a really useful tool for you as a user — for routines automatization e.g.

## Shell

Software that interprets your textual input in command line. It also handles your shortcuts (e.g. Ctrl + D or arrow keys) and prints command prompts (something like `user@home:~$`).

Shell also supports *scripts* — a kind of programs that describes shell behaviour as if user interacting with it.

Notable examples of shells are Bash (Linux) and PowerShell (Microsoft® Windows®).

## Daemon

Software that is intended to run in background, without any direct user control. In most cases daemons should be started at the system startup or at least once user logged in.

Names of daemon applications usually end with `d`, e.g. `sxhkd`, `syslogd`, `firewalld` and so on, but you should not confuse it with some of system directory names that ends with dot-d `.d`, e.g. `conf.d`.

## Package Manager (PM)

Software that provides a unified way to obtain, install and remove so-called *packages*: archived files that contain additional software or it's resources (configuration, icons, themes etc.) With package manager you don't have to manually install bunch of `setup.exe`s: instead, you can just run something like `apt-get install [list of software...]` once and get all you need. If needed, you can also update or remove software in similar fashion.

Package managers are a common feature for most of Linux distributions. Primary interface for most of package managers is command line:

| Distribution     | Package Manager            | Package Format |
| ---------------- | -------------------------- | -------------- |
| Debian family    | APT (known as `apt-get`)   | `*.deb`        |
| Fedora family    | DNF (replacement to `yum`) | `*.rpm`        |
| ArchLinux family | pacman                     | `*.pkg.tar.xz` |
| Void             | XBPS                       | `*.xbps`       |

On Microsoft® Windows® there are no any native package managers currently. You can use [Chocolatey](https://chocolatey.org/) though, but it's a third-party software and it still lacks some common PM features.

One of main package managers' feature is dependencies handling. For instance, if an application `foo` from `foo.pkg` package depends on some resources from `bar.pkg`, then manager should retrieve both of these packages when user commands to install `foo` software.

Some of packages are called *meta*. This means that they don't provide any actual resources, but list of dependencies only. Metapackages are useful when you want to install the whole set of applications at once, e.g. in case of desktop environment installation.

When package manager obtains a package, most likely it downloads a package from one of repositories which are hosted on some remote servers, so in most of cases you'll need stable internet connection to install packages. Alternatively, you can set up and use the local mirror, but it's not that easy.

In Void, you should type `xbps-install [packages...]` in command line if you want to install packages and `xbps-remove [packages...]` if you want to remove them.

## Package Repository and Maintainers

Package repository is a special server (remote most likely) where all the packages are stored. There are also *mirror* repositories that replicates all the original repository contents.

Package maintainer is a person that controls package(s) building process. Specifically to Void, he (or she) writes building scripts and applies necessary patches on original software sources.

# Display Server (Xorg, X11, Wayland, Weston etc.)

Software that creates all the graphical mode output (opposite to default textual mode).

It basically handles all the graphical applications output and user keyboard/mouse/touchpad/whatever input events that happens in graphical mode. There are other applications that handle user input too (e.g., sxhkd shortcut daemon), but display server handles it primarily by default.

**Xorg** (also known as X.Org, X11 or something like that) is a classic display server which development began in 1984. It's still considered as default display server, extremely stable and reliable. You can install Xorg with `xorg` package in most of distributives, including Void.

**Wayland** is a new protocol for modern display servers (they're called "compositors" in Wayland terminology), e.g. for Weston or KWin. I personally don't recommend to use such servers for now: according to [Wikipedia](https://en.wikipedia.org/wiki/Wayland_(display_server_protocol)), Wayland first stable release was in summer of 2017 and it still lacks some software (e.g. mature window managers) as well as user issues/solutions base.

## Window Manager (WM)

Software that handles all the displayed windows separately. More precisely, it controls each window screen position, size and decorations (borders, title and buttons like minimize/maximize/close).

While window manager is an optional component for display server, it should be installed in any Linux system if you want to comfortably work in graphical mode. There are many window managers, most of them are made for Xorg and they wouldn't work on Wayland-based servers. Some window managers are designed as a part of desktop environment (e.g., Xfwm is part of XFCE), some are designed for separate use (like Openbox).

There are at least two types of window managers:

  - **Floating** window managers implements classical conception of *floating* windows. This conception is common e.g. for Microsoft® Windows® interfaces, where user can control windows primarily with mouse, i.e. drag, move, resize, close via title buttons and so on. Examples: "\*-boxes" (Openbox, Fluxbox etc.), Xfwm, FVWM.
  - **Tiling** window managers implements advanced (more hard for novice users) conception of *tiling* windows. Such windows are automatically tiled depending on its' number and layout specified. They're primarily designed for keyboard usage, and better for people that work with texts a lot (programmers e.g). Examples: i3, xmonad, bspwm.

There are also **mixed** tiling managers which implement both conceptions, but their number is extremely small.

## Composite Manager (CM)

Software that handles optional and external window effects, such as transparency, border shadows, fading, background blur and so on. Sometimes it can also help with the tearing problems (i.e. when window contents randomly flickers and updates unevenly); however in case of such problem you better check graphic driver settings first (in `/etc/X11/xorg.conf` e.g).

Most of composite managers are built into window managers or even in desktop environments. However, there are also some standalone options: you can use e.g. dead simple Xcompmgr or more advanced Compton.

## Desktop Environment (DE)

Just a set of different software designed to work together. Usually includes some basic user applicatons like file manager, text editor, system settings interface and other tools which have the same theme, look and feel.

Currently most popular desktop environments are [GNOME](https://www.google.com/search?tbm=isch&q=gnome+desktop+environment) and [KDE](https://www.google.com/search?tbm=isch&q=kde+desktop+environment). There are also lightweight options like [Cinnamon](https://www.google.com/search?tbm=isch&q=cinnamon+desktop+environment) or [XFCE](https://www.google.com/search?tbm=isch&q=xfce+desktop+environment) and modern bleeding-edge variants like [LXQT](https://www.google.com/search?tbm=isch&q=lxqt+desktop+environment) or [Budgie](https://www.google.com/search?tbm=isch&q=budgie+desktop+environment), and many, many others.

Desktop environments are nice for Linux beginners or when you don't want to set up all the things by yourself. However, they're usually more bloated comparing to custom user application sets and thus takes more system resources. This might be critical for old or ultra-compact machines.
