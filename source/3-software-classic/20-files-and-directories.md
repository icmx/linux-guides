# Files and Directories

## Navigation

### `ls` — List Files

```
  ls [options...] [targets...]
```

Print *target* directory(es) contents.

Options:

  - `-a` print all, even hidden objects
  - `-R` print recursively (with subdirectories)
  - `-l` long listing (file per line, lots of info)
  - `-h` human-readable (for file size in `-l`)

### `cd` — Change Directory

```
  cd [target]
```

Change current directory to *target*. Will use home directory if *target* isn't specified.

### `less` — View File Contents

```
  less file
```

Interactively displays a *file* contents. This tool is newer alternative for `more` text viewer, that's why it's got such strange name. Similar commands are called "pagers" sometimes.

Navigation within:

  - `h`: get detailed navigation help
  - Arrow Up, Arrow Down, j and k: scrolling
  - `/pattern`: search for a *pattern* (regular expressions and backslashing are supported).
  - `n`, `N`: move to next or previous occurence.


### `file` — Determine Type

```
  file [options...] targets...
```

Options:

  - `-i` Print *target* type as in MIME format (e.g. `image/png`)
  - `-k` If *target* suits for multiple types, then print all of them, not only one
  - `-z` Try to uncompress data before detecting

Despite the name, this tool works also for directories and links.

## Creation

### `touch` — Create or Update File

```
  touch targets...
```

Creates new *target* empty file(s) or update access time for old one(s). Directories access time can be also updated with this tool.

### `mkdir` — Make a Directory

```
  mkdir [options...] targets...
```

Option `-p` creates directrory parents too (even if they're not exist). It's useful when you e.g. need to create multiple nested directories at once, like `~/Music/Kraftwerk/Man-Machine`.

## Management

### `cp` — Copy

```
  cp [options...] source target
```

Options:

  - `-r` recursive (all the directory contents)
  - `-v` verbose (print every operation)
  - `-u` update (copy only if target doesn't exist or older than source)
  - `-n` don't overwrite existing files

One must set `-r` option to copy the directory.

### `mv` — Move

```
  mv [options...] source target
```

Options:

  - `-n` don't overwrite existing files
  - `-u` update (move only if source newer than target or target doesn't exist)
  - `-v` verbose (print every operation)
  - `-f` force (do not prompt before overwriting)

Unlike `cp` command, `mv` don't need a recursive flag to move the directory.

### `rm` — Remove

```
  rm [options...] target
```

Options:

  - `-r` recursively (all the directory contents)
  - `-f` force (even write-protected, with no messages)
  - `-i` intercative (opposite to `-f`, prompts the user confirmation)

**Use it with caution**. Never do `rm -rf` for root `/`, home `~` or similar *targets*.

### `ln` — Link

```
  ln [options...] source target
```

Creates link object located in *target* and refering to *source*, so system will be able to use *target* while actual resource is placed in the *source*.

You can link both to files and directories.

Option `-s` makes symbolic links instead of hard ones —  that's what one need at most of time.

## Archiving and Compression

### `tar` — Archive

```
  tar [options...] target [source]
```

Options:

  - `-c` create new TAR
  - `-x` extract existing TAR
  - `-t` print TAR table of contents
  - `-f` specify *target* TAR file name
  - `-k` keep original files in TAR (not overwrite)

Examples:

  - `tar -c -f backup.tar file-1 file-2 file-3` create TAR (`backup.tar`) with files `file-1`, `file-2` and `file-3`
  - `tar -x -f backup.tar` extract previous TAR contents to current directory

TAR format just packs all the files into single one, while ZIP makes them compressed.

### `gzip` — Compress

```
  gzip [options...] file
```

Options:

  - `-1`..`-9` set compression speed/quality mode. Fastest option is `-1` while `-9` makes best compression. Default value is `-6`.
  - `-d` decompress file instead of default compression.
  - `-k` keep original files after successful compression or decompression. By default `gzip` will remove them.

`gzip` compression only work with single file. To compress multiple files, use `tar` command before compression or switch to advaced archivers like `7z`.

## Search

### `locate` — Static

```
  locate [options...] patterns...
```

Option `-i` makes `locate` ignore case in *pattern(s)*.

This tool works in *static* manner and thus requires index database. You should run `updatedb` as `root` at least once to use `locate` correctly. Better to set up some service or `cron` job to update database periodically.

### `find` — Dynamic

```
  find target [options...] [query...]
```

*Target* shound be any directory, use dot `.` for current.

#### Queries

You can find files or directories by specifying one or multiple queries:

##### Queries with Parameter

  - `-name` search by object name specified (case sensitive), or `-iname` (insensitive)
  - `-size` search by object size specified (`c` for bytes, `k` forkilobytes, `M` for megabytes, `G` for gigabytes, e.g. `1024`)
  - `-atime`, `-mtime` search by access or modification time specified in `n` × 24 hours (e.g. `2` means 48 hours ago)
  - `-type` search by object type: file (`f`), directory (`d`) or link (`l`)
  - `-user` search by object user name or UID (user ID)
  - `-group` search by user object group or GID (group ID)

##### Queries without Parameter

  - `-empty` search an objects that has no any content (empty file or directory)
  - `-readable`, `-writable` or `-executable` search objects by user-related attributes (first three `r`, `w` and `x` in attributes list respectful)

#### Operators:

  - `( query )` force *query* presedence, probably should be escaped by backslashes `\( query \)` due to shell internal parenthesis
  - `-not query` inverse *query* results (standard logical `NOT` operation)
  - `query-1 -and query-2 -and query-3 -and ...` find files that match all the *queries* specified (standard logical `AND` operation)
  - `query-1 -or query-2 -or query-3 -or ...` find files that match at least one of queries specified (standard logical `OR` operation)
