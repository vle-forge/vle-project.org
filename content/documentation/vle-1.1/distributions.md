+++
categories = []
date = "2015-11-21T16:09:23+01:00"
description = ""
keywords = []
title = "Distributions"

+++

A distribution is a set of [packages]({{< ref
"documentation/vle-1.1/packages.md">}}) available on an URL and a description
file `packages.pkg`. For an example, you can look at the [VLE distribution]({{<
ref "documentation/vle-1.1/vle-packages-distribution.md">}}).

# How to use a distribution

To use a package distribution you have to add a remote URL into your `vle.conf`
file (see the remote preferences of [vle.conf documentation]({{< ref
"documentation/vle-1.1/configuration-file.md">}}). 
Be careful to add only URLs that you trust in. For example to add an URL of a
distribution `http://mydistrib/`, update the following line

```
vle.remote.url=http://www.vle-project.org/pub/1.1
```

With:

```
vle.remote.url=http://www.vle-project.org/pub/1.1,http://mydistrib/
```

Then you have to perform an update of the local view of the remote packages:

```bash
vle --remote update
```

To install packages from this distribution you can use the remote mode the [vle
CLI] (VLE-Application-for-vle-1.1).

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
the packages contained into the distribution (see [packages]({{< ref
"documentation/vle-1.1/packages.md">}}) structure). For example:

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
Url: http://www.vle-project.org/pub/1.1
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
Url: http://www.vle-project.org/pub/1.1
Size: 0
MD5sum: xxxx
```

The `tar.bz2` files are compressed archives of the source code of 
packages. For the moment only source code is provided into distribution.


