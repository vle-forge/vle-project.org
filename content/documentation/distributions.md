+++
topics = ["documentation"]
date = "2016-12-16T12:32:04+01:00"
description = ""
tags = ["vle-2.0","package","distribution"]
title = "Distributions"
+++

A distribution is a set of [packages](../packages) available on an URL and a
description file `packages.pkg`. For an example, you can look at the [VLE
distribution](../../packages).

# How to use a distribution

To use a package distribution you have to add a remote URL into your `vle.conf`
file (see the remote preferences of the [vle.conf
documentation](../configuration-file). Be careful to add only URLs that you
trust in. For example to add an URL of a distribution `http://mydistrib/`,
update the following line:

```
vle.remote.url=http://www.vle-project.org/pub/2.0
```

With:

```
vle.remote.url=http://www.vle-project.org/pub/2.0,http://mydistrib/
```

Then you have to perform an update of the local view of the remote packages:

```bash
vle --remote update
```

To install packages from this distribution you can use the remote mode of the
[command line interface](../vle-cli).

# Content of a distribution

The content of a distribution should have the following structure.

```
$http://mydistribution/
  └─ packages.pkg          ; the package description file
  └─ mypkg1.tar.bz2        ; the first package of the distribution
  └─ mypkg2.tar.bz2        ; the 2nd package of the distribution
  └─ ...
```

The `packages.pkg` is simply the concatenation of the `Description.txt` files of
the packages contained into the distribution (see [packages](../packages)
structure). For example:

```
Package: mypkg1
Version: 0.1.0
Depends:
Build-Depends:
Conflicts:
Maintainer: John Do <jdo@company.net>
Description: An extension to build difference equation models
 .
Tags: extension
Url: http://www.vle-project.org/pub/2.0
Size: 0
MD5sum: xxxx
Package: mypkg2
Version: 0.1.0
Depends:
Build-Depends:
Conflicts:
Maintainer: John Do <jdo@company.net>
Description: An extension to build FSA models
 .
Tags: extension
Url: http://www.vle-project.org/pub/2.0
Size: 0
MD5sum: xxxx
```

The `tar.bz2` files are compressed archives of the source code of
packages. For the moment only source code is provided into distribution.
