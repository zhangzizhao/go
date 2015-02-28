# Golang Dependency Management Patch

Lock Golang packages by adding ``#revision`` to the import path. 

```bash
go get github.com/mattes/migrate#v1.2.0
```

The command above would clone the ``migrate`` package to 
``$GOPATH/src/github.com/mattes/migrate#v1.2.0`` and checkout ``v1.2.0``.

Use multiple versions of the same package in the same project or in
different projects. No need to modify ``$GOPATH``!

```go
import (
  "github.com/mattes/migrate" // latest master branch
  oldMigrateAlias "github.com/mattes/migrate#v1.2.0"
  anotherAlias "github.com/mattes/migrate#c1f0a1a04441f8508826792616a6cb0f65968283"
)
```

### This is experimental ...

Not sure if it makes sense at all as this would break
the existing ``go get`` implementation.

Tested a little bit with ``go version go1.4.2 darwin/amd64``.

# __PRs/ Feedback/ Ideas welcome!__
### __https://github.com/mattes/go/pull/1__


## Apply patch

```bash
# find original get.go and vcs.go and change to this directory
cd /usr/local/Cellar/go/1.4.2/libexec/src/cmd/go # if installed with brew

# apply patch
patch < fix-dependencies.patch

# find make.bash and rebuild go
cd /usr/local/Cellar/go/1.4.2/libexec/src
./make.bash
```


## Create patch (as needed)

```bash
# create patch 
git format-patch release-branch.go1.4 --stdout > fix-dependencies.patch
```