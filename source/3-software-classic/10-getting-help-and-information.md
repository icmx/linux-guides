# Getting Help and Manuals

### Help Options

You can use these options to get short usage info for command:

```
command --help
command -h
command -?
command --usage
```

Examples:

  - `tr --help`
  - `ping -h`

Not all the commands support such options, but most of them for sure.

### *whatis* — Short Info

```
whatis [options...] objects...
```

Options:

  - `-w` treat each target as a shell pattern style wildcards (`*`, `?`)
  - `-r` treat each target as a regular expression (`.*`, `.+`)

### *man* — Detailed Info

```
man [options...] [section] object
```

*Object* may be a command or file sometimes. Option `-K` searches for specified string in all of manual pages

Sections available (optional):

  1. User commands
  2. System calls
  3. Library calls
  4. Special files
  5. File formats and conventions
  6. Games
  7. Miscellaneous
  8. Aministration tools

If section isn't specified, then `man` will enumerate through the all available sections until reach one.

See `less` command for navigation within `man` pages.
