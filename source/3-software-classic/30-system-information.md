# System Information

## Date and Time

### *date* — Current Time

```
date [options...] [+format]
```

Options:

  - `-d` set specific date to display (instead of curent date)
  - `-s` set system date (only works under `root` user)

Formatting:

  - `%c` Local date and time, e.g. `Wed Nov 1 12:34:01 2017`
  - `%F` Full date in ISO format, e.g. `2008-09-20`
  - `%R` Full time in ISO format. e,g, `01:43`
  - `%A` weekday name, e.g. `Monday`
  - `%B` month name, e.g. `January`
  - Format example: `+%Y-%m-%d %H:%M`, like `2007-09-20 01:43`

There are many of format options available, consult the `man date` for more.

### *time* — Execution Time

```
time [command]
```

When *command* will over, prints its execution time:

  - `real`: actual elapsed time to execute
  - `user`: CPU time spent for user (non-kernel) operations
  - `sys`: CPU time spent for kernel operations

### *uptime* — Operating Time

```
uptime [options...]
```

Options:

  - `-p` print in pretty format (more clean uptime only)
  - `-s` print uptime since moment specified in `YYYY-MM-DD HH:MM:SS`

Default output format:

```
current-time    uptime    users-number    load-averages
22:05:16 up     10:47,    2 users,        0.46, 0.56, 0.57
```

*Load averages* are three integers at the end of output that represents average system load level for 1, 5 and 15 minutes. These values representation are highly depends on CPU used: roughly, `1.0` means 100% load for single-core, 50% for dual-core and 25% for quad-core CPU systems.

## Paths and Names

### *whoami* — Current User

```
whoami
```

Prints current user name.

### *which* — `$PATH` Used Binary

```
which commands...
```

Print full path to executable file(s) referred to *command(s)*, e.g. `which ls` prints `/usr/bin/ls`.

### *whereis* — Command Components

```
whereis [options] command
```

Options:

  - `-b` search executable files (binaries) only
  - `-m` search manuals only
  - `-s` search sources only

### *w* — Logged Users and Uptime

```
w [options...] users...
```

Option `-s` displays in shorter format

## System and Resources Usage

### *uname* — Basic System Info

```
uname -a
```

There are other options except of `-a`, consult the `man uname` for details.

### *df* — Filesystem Usage

```
df [options...] directories...
```

This will print file usage information for filesystem(s) mounted on *directory(es)* specified.

### *du* — Directory Usage

```
du [options...] directories...
```

Options:

  - `-s` display only total usage info for all items
  - `-c` display additional total line

### *free* — RAM Usage

```
free [options...]
```

Options `-b`, `-k`, `-m` and `-g` displays in bytes, kibibytes, mebibytes and gibibytes

* * *

Note: there is `-h` option for *df*, *du* and *free* commands: it makes them print their output in human-readable format.
