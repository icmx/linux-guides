# Package Management

> **\* Void-specific**
>
> Void Linux uses custom XBPS package management system. Other Linux distributions probably uses their own package managers (e.g. APT, DNF etc.)

### Search — *xbps-query*

```
  xbps-query [options...] package-query
```

Options:

  - `--property` search packages only with property specified
  - `--regex` match strings using [regular expressions](#)
  - `--fulldeptree` print all the package dependencies

### Install — *xbps-install*

```
  xbps-install [options...] package-queries...
```

### Remove — *xbps-remove*

```
  xbps-remove [options...] package-queries...
```

### Package Queries

You can specify package using simple *package-query* synatax while using `xbps-query` and `xbps-install`:

  - By package name, e.g. `wine`
  - By package name and exact version, e.g. `wine-2.20`
  - By package name and version with comparator, e.g. `wine>=2.20`
