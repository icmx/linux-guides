# Shell

> **TODO**
>
>   - Functions
>   - Exporting, sourcing, rc-files
>   - Expansion for `~`, `*`, `?`, `[a,b,c]`, `{a,b,c}`
>   - Expansion for `${}` and `$()`
>   - Maybe split all this

While you're working with command line interface, you're actually working in a shell – a special kind of software that handles and parses all of user input, including typed text and shortcut events (even arrow keys that moves carret).

There are lots of different shells. As Linux user you should know at least these two:

  - *Bourne Again Shell*, better known as *Bash*. Considered as classic and default shell for almost any Linux distribution (and Void Linux too), it's simple yet flexible shell for generic users.
  - *Debian Almquist Shell*, or *Dash*. Althrough it have "Debian" in its name, this shell is actually multi-distributive and installed by default in Void too. This lightweight shell has no any human-oriented functions like auto-completion, keyboard shortcuts handling or color highlighting – instead, it provides fast experience which is actual for long standalone scripts.

There are other even more advanced shells also, Z shell or fish shell for instance. However, I personally don't recommend you to use them: despite speed and usability improvements (comparing to Bash), you're actually won't see any diffrence. Custom shells are real overkill for generic non-power users like you and me.

> **\* Void-specific**
>
> Default root shell for Void is Dash. It's not as easy as Bash for human use (there is even no history!), but I definitely don't recommend you to change default shell. Instead, type just `bash` once you're logged as root user — this will open new Bash session for root.

## Anatomy of Shell

### Prompt

That thing you see from the left side of each command. It's intended to *prompt* your current status (or context) as a user in system. Bash prompt looks similar to this:

```
         it's all prompt
┌────────────────────┴─┐
curly@dragon:~/Pictures$ ls -la --color=always -- /home/curly█
```

It means the folowing:

  - Your account name is `curly`
  - Your PC name is `dragon`
  - Your working directory is `~/Pictures`. This path actually points to `/home/curly/Pictures` since tilde `~` means current user home directory. This directory will be used any comands while performing, e.g. `mkdir Butterflies` command will create `Butterflies` directory right in the `~/Pictures`.

In Bash, one can redefine prompt structure to display e.g. only current directory name by modifying the special `$PS1` variable.

### Command

Command is what user types right after the prompt. Typically it looks like this:

```
                                             it's all command  carret
                         ┌────────────────────────────────┴─┐ ↙
curly@dragon:~/Pictures$ ls -la --color=always -- /home/curly█
```

Usually, any command consists of following elements:

```
name [options...] [targets...]
```

*(brackets means that elements are optional and may be defined multiple times)*

#### Name

Command name is something like  `cd`, `ls`, `mkdir`, `ping` etc. It refers to a real executable file name, e.g. `ls` is actually `/usr/bin/ls` file. Once name is parsed by the shell, it will be searched in directories that specified in `$PATH` shell variable.

#### Options

Command options are space separated key-value pairs also known as command arguments, flags, keys, operands, parameters or switches. There are some features that you should consider:

  - Options have a key and optional value, e.g. `-k value` or `--key value`.
  - Key can be started with dash or two, e.g. `-k` (short one-char form) or `--key` (long form).
  - Multiple short options can be combined, e.g. `-a -b -c` are same to `-abc`.
  - Key can be connected with value by equality sign, e.g. `-a=0`. It that case, there should not be spaces around the equality sign.
  - Values can be quoted with single or double quotes, e.g. `-a "file name"` or `--param='value with spaces'`.
  - Options list can be manually terminated with empty two dashes `--` option, so text after `--` will be treated as `target` part of command. Normally you don't have to do that, but sometimes you can e.g. face with files which names are similar to options keys. In that case `--` will be useful.

All these options features are not strict rules, but more like style arrangements. There are some exceptions like `dd` or `tar` commands which have their own options style.

#### Target

Techically last and main option with no key, mostly is file name or some kind of destination.

  - Most of commands allows multiple targets separated by spaces.
  - Target or option value containing spaces must be quoted with single or double quotes like `"long target or value name"` or escaped like `long\ target\ or\ value\ name`. It's because spaces are considered as values separators by default.

#### Example

```
                     name              options         target
                         ↘  ┌──────────────┴─┐    ┌───────┴─┐
curly@dragon:~/Pictures$ ls -la --color=always -- /home/curly█
                                               ↗
                               empty two dashes
```

  - Name: `ls` (actually `/usr/bin/ls`)
  - Options:
    - `-la` means `-l` (long listing) and `-a` (list all, including hidden files). These options are combined and both have no any value.
    - `--color=always` add colors to output (depends on file or directory type)
  - Options list manually terminated with `--`. Just for demonstration, in current case it's not necessary.
  - Target: `/home/curly` (home directory of user named `curly`, better to use e.g. `~`)

### Control Keys

Like other shells, Bash is entirely driven by keyboard:

  - `Left`, `Right`: move a carret left or right
  - `Enter`: execute command that you've just typed
  - `Up`: select previous command form history (if any)
  - `Down`: select next command form history (if any)
  - `Tab`: try to complete a command
  - `Tab` × 2: print available completions (for command or files, if any)
  - `Ctrl` + `R`: search in commands history, `Ctrl` + `R` one more time for another search entry
  - `Ctrl` + `W`: erase last word in command line
  - `Ctrl` + `U`: erase command line
  - `Ctrl` + `L`: erase all the visible shell space to clean screen (same as `clear` command)
  - `Ctrl` + `D`: log out of current session (same as `exit` command)
  - `Ctrl` + `C`: stop currently running process
  - `Ctrl` + `Z`: pause currently running process

### Variables

Shell variables are special values that one can get or set while using the shell. They works like string variables in programming languages, but in little simplified manner.

To *set* variable, one have to just type something like `NAME="value"`, where `NAME` is variable name. There should not be a whitespace between the name, equality sign `=` and value.

To *get* and use variable somewhere, one have to type variable name with dollar sign `$` at the beginning, like `$NAME`. Here are detailed example:

```sh
name="curly"
shell="bash"

echo "Hi! My name is $name and I use $shell"

# Will print: "Hi! My name is curly and I use bash"
```

One can append variables from start or end:

```sh
color="red"
color="blue and $color"
color="$color and green"

echo "$color"

# Will print: "blue and red and green"
```

#### Built-ins

Some values are already built in the shell:

  - Read-only (you can't modify these, at least directly):
    - `$UID` current user id, e.g. `1000`
    - `$USER` current user name, e.g. `curly`
    - `$HOME` current user home directory, mostly probably it's equal to `/home/$USER` (e.g. `/home/curly`), except root user which home is `/root`
    - `$PWD` current working directory, alternative to `pwd` command
    - `$HOSTNAME`: current machine name
    - `$RANDOM` random integer number in 0..32767 range, it will be random at any access.
  - Writable:
    - `$PS1` and `$PS2`: structures for primary and secondary prompts, see below
    - `$PATH` colon-separated list of directories for executable files, e.g. `/usr/local/bin:/usr/sbin:/sbin:/bin`.

##### Structure of `$PS1` and `$PS2`

Default value of `$PS1` variable is `\u@\h:\w\$`, which is shows up like `curly@dragon:~$` in examples above. Backslashed characters like `\u` are called *escape sequences* and have special meaning:

  - `\u` — current user name, e.g. `curly`
  - `\h` —  current machine name, e.g. `dragon`
  - `\w`, `\W` current working directory full path (`/home/curly/Pictures`) or just name (e.g. `Pictures`) respectively
  - `\t`, `\T` and `\@` — current time in different formats
  - `\d` — current date, e.g. `Tue May 26`
  - `\$` — prints `$` for generic user and `#` for root
  - `\n` — newline character
  - `\\` — literal backslash

In its turn, `$PS2` shows up when shell receives new line charater (i.e. user hits Enter), but command seems not finished yet, like this:

```sh
echo "say
```

Shell expects for closing quote which will end the command — to indicate that, `$PS2` will be printed before a user input:

```
                    $PS1
┌────────────────────┴─┐
curly@dragon:~/Pictures$ echo "say
> something"
 ↖
  $PS2 character
```

Default value of `$PS2` is just a `>` character.

> **\* Dash-specific**
>
> Dash shell is not working with escape sequences. Its default `$PS1` value is just `$` or `#` (depending on privileges level)

##### Structure of `$PATH`

As it said, `$PATH` contains colon-separated list of directories where system executablee files are stored. One can easily check it in any time:

```sh
echo "$PATH"

# Will print something like: "/usr/local/bin:/usr/sbin:/sbin:/bin"
```

When someone enters a command, e.g. `ping example.org`, all the text up to first space (i.e. `ping`) will be used to search in `$PATH` directories – and if file with such name exists, then it will be executed. If there are two files with the same name, e.g. `/usr/local/bin/ping` and `/bin/ping`, then file from first `$PATH` entry will be executed (i.e., `/usr/local/bin` has higher priority for current `$PATH` case).

One can add a custom executable files directory by appending `$PATH` value at any time:

```sh
# Suppose curly have /home/curly/bin directory wtih executables

PATH="/home/curly/bin:$PATH"
```

That's it. Now executable files will be searched in `/home/curly/bin` directory too.

*Note*: to make executable files available as a commands, one should also add a permission to execute (`x`) to such files.
