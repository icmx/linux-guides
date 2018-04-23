# Text Operations

> **TODO**
>
>   - awk
>   - sed
>   - vi
>   - grep
>   - cat
>   - tee

### `echo`

```
  echo [options...] text...
```

Prints specified *text*, to standard output (terminal) by default. One of most popular commands, it's widely used e.g. to print basic information into terminal or file.

Options:

  - `-n` do not print trailing newline character `\n` (it's printed by default).
  - `-e` enable support of backslashed characters (to interpret color sequences and other special characters e.g., see `man echo` for more)

### `cut`

```
  cut [options...] files...
```

Cuts all the input lines by specified mode and range.

Options:

  - `-b` cut by bytes
  - `-c` cut by characters
  - `-f` cut by fields
  - `-d` specify delimiter character (for `-f` option)

You can specify only one type of cutting (`-b`, `-c` or `-f`). There should be a range specified after type, in one of these formats:

  - `N` N'th only, counted from 1
  - `N-` from N'th to end of line
  - `N-M` from N'th to M'th (included)
  - `-M` from first to M'th (included)

You can specify multiple ranges at once separating them by commas `,`.

Examples:

  - `cut -f 1,5,7 -d ":" /etc/passwd` print all the system user (login names, commest and login shell) stored in `/etc/passwd` file.
  - `echo $PATH | cut -f 3- -d ":"` print last three (`3-`) entries of `$PATH` environment variable.

### `head` and `tail`

```
  head [options...] file
  tail [options...] file
```

`head` prints file beginning and `tail` prints file ending. These commands are pretty similar and have the same options.

Options:

  - `-n` set specific lines number to print
  - `-c` set specific bytes count to print
  - `-f` follow the file changes and append data as the file grows
  - `-s` set the interval for `-f` option in seconds (default is *1.0*)

### `rev`

```
  rev files...
```

Copy the file or stream in reverse order.

### `seq`

```
  seq [options...] first [increment] [last]
```

Prints a sequence of numbers starting from *first*, in steps if *increment* and ending with *last* (or less or equal to *last* when *increment* specified).

Options:

  - `-f` set output format in `printf` floating point number manner
  - `-s` set separator betheen numbers (by default it's a newline `\n`)
  - `-w` print also leading zeroes to equalize the numbers width (e.g. `00`, `01`, `02`, ... `10`)

### `shuf`

```
  shuf [options...] file
```

Permutate input lines in random order.

Options:

  - `-r` allow lines to be repeated
  - `-n` set lines number (≤ input lines number)

### `sort`

```
  sort [options...] files...
```

Options:

  - `-f` ignore input case
  - `-h` sort numbers in human-readable form (i.e. `1 2 3 10 20 30` instead of `1 10 2 20 3 30`)
  - `-r` reverse sort
  - `-c` check for sorted input and point an error (if any), not sort

### `tr`

```
  tr [options...] set-1 [set-2] file
```

*No description provided*.

### `uniq`

```
  uniq [options...] input [output]
```

Prints unique, duplicate or number of such lines count.

Options:

  - `-i` ignore case when comparing
  - `-c` print also number of occurences before the lines
  - `-d` print only duplicate lines
  - `-u` print only unique lines (this is by default)

### `wc`

```
  wc [options...] files...
```

Prints count of bytes, chars or lines in file specified.

Options:

  - `-c` count bytes
  - `-m` count chars
  - `-w` count lines

You can specify multiple options and files (additional `total` line will be printed if multiple files specified).

### `dd`

```
  dd [options...]
```

Copies content or redirect stream from *source* to *target*.

Options:

  - `if` set *source* file, stantard input by default. In most of cases it should be an ISO image file or device file like `/dev/zero`
  - `of` set *target* file, standart output by default. In most of cases it should be device file like `/dev/sdc` or `/dev/null`
  - `bs` bytes speed upper limit, most popular value is `4M`
  - `status`: may be a `none`, `noxfer` for final stats or `progress` for stats during the process.

Example: `dd if=/dev/zero of=/dev/sdX`. This will overwrite the `/dev/sdX` device with nulls. **Warning**: don't use it for tests, `dd` may erase your data!

Notice: `dd` uses strict `key=value` options syntax instead of generic `--key value`.
