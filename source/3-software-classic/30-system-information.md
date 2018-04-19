# System Information

## Date and Time

### `date` — Current Time

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

### `uptime` — Operating Time

```
  uptime [options...]
```

Options:

  - `-p` print in pretty format (more clean uptime only)
  - `-s` print uptime since moment specified in `YYYY-MM-DD HH:MM:SS`

## Paths and Names

### `whoami` — Current User

```
  whoami
```

Prints current user name.

### `which` — `$PATH` Used Binary

```
  which commands...
```

This will print full path to executable file(s) referred to *command(s)*, e.g. `which ls` prints `/usr/bin/ls`.

### `whereis` — Command Components

```
  whereis [options] command
```

Options:

  - `-b` search executable files (binaries) only
  - `-m` search manuals only
  - `-s` search sources only

### `w` — Logged Users

```
  w [options...] users...
```

Option `-s` displays in short format (more human-readable)

## System and Resources Usage

### `uname` — Basic System Info

```
  uname -a
```

There are other options except of `-a`, consult the `man uname` for details.

### `df` — Filesystem Usage

```
  df [options...] directories...
```

This will print file usage information for filesystem(s) mounted on *directory(es)* specified.

### `du` — Directory Usage

```
  du [options...] directories...
```

Options:

  - `-s` display only total usage info for all items
  - `-c` display additional total line

### `free` — RAM Usage

```
  free [options...]
```

Options `-b`, `-k`, `-m` and `-g` displays in bytes, kibibytes, mebibytes and gibibytes

* * *

Note: there is `-h` option for `df`, `du` and `free` commands: it makes them print their output in human-readable format.
