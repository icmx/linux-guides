# Users and Access Rights

## Users

### Create — `useradd`

```
  useradd [options...] logins...
```

### Modify — `usermod`

```plain
usermod [options...]
```

### Remove — `userdel`

```
  userdel [options] login
```

## Management

### Password — `passwd`

```
  passwd [options...] user
```

Options:

  - `-d` delete user's password
  - `-S` show status only, not change
  - `-a` show statuses for all users

### Change Owner and Group — `chown`

```
  chown [options...] owner[:group] targets...
```

One can type just `owner` or `:group` to change them separately.

### Change Mode (Permissions) — `chmod`

```
  chmod [options...] permissions... targets...
```

Each permission consists of one (or more) class, one (or more) modes and one operator between them. You can also combile multiple permissions with commas `,` (see examples below).

Classes:

  - `u` user (*target(s)* owner)
  - `g` group (user's group members)
  - `o` others (all other users)
  - `a` all of it (same as `ugo`)

Operators:

  - `+` add new mode(s)
  - `-` remove old mode(s)
  - `=` set only specified mode(s)

Modes:

  - `r` read
  - `w` write
  - `x` execute

Examples:

  - `chmod ug+w file` makes user and group able to write into `file`.
  - `chmod go=rw file` makes group and others able to read and write only (removes all previous permissions for group and others if any).
  - `chmod u-x file` makes user unable to execute `file`.
  - `chmod -R u=rwx,g=rw,o-rwx directory` makes separate permissions for all the three classes.

`chmod` also supports octal and binary permissions schemas, but they are too complicated for daily use.

Both `chown` and `chmod` has an `-R` option for recoursive changing which is might be useful for directories.

## Substitution

### Default Substitute — `su`

```
  su [options...] [user]
```

Option `-c` set command to execute as another user, then switch back at the command end. If no *user* is specified, then `root` will be assumed.

> **Security note**
>
> In my opinion, default `su` usage may be quite unsafe by some reasons. To avoid `$PATH` and binaries substitution, one can use the following synopsis:
>
> ```
>   /bin/su --login user [options...]
> ```
>
> In that case, `/bin/` will absolutely point to original `su` command binary and `--login` option will additionally reset previous user environment variables, including `$PATH`.

### Advanced Substitution — `sudo`

```
  sudo [options...] command
```

Option `-u` set user to run the command (`root` by default).

#### Sudoers File

Sudoers (*/etc/sudoers*, */etc/sudoers.d*) is a file that defines *sudo* behaviour. Its main part are *rule definitions*. Such definitions have the following syntax:

```plain
user host=(runas) options commands
```

  - *user* — user or group of users on which that rule is applied. Group name must be started with percent character, e.g. `%wheel`.
  - *host* — host on which this rule is allowed, or `ALL` for any host.
  - *runas* — allow to execute the commands only as users listed in *runas*. `ALL` will let one execute any command as any specified user with `sudo -u user` (root is considered as default in `-u` option).
  - *options* — options list for current rule, e.g. NOPASSWD will let one execute commands without asking a password. Multiple options
 must be separated by space. Any option consist of key and value separated by colon. If value is not available (like in NOPASSWD), then option just ends with colon.
  - *commands* — list of commands which may be executed within this rule. Multiple commands must be separated by comma. `ALL` instead of commands means any command available in a system.

One can also define the so-called aliases by following syntax:

```plain
type NAME = items
```

  - *type* — alias type:
    - User_Alias — for users list
    - Host_Alias — for hosts list
    - Runas_Alias — for runas users list (see *runas* part above)
    - Cmnd_Alias — for commands list
  - *NAME* — name of alias, must use only uppercase letters, numbers and underscores.
  - *items* — users, hosts, runas users or commands, separated by comma.

### Notes

`su`, `sudo` and `passwd` commands requires password while execution. That password will not be shown (at all, even traditional asterisks like `******`) while typing.
