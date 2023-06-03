# Install

The Warp CLI is available in several popular package managers. It's also [available](https://github.com/warpdl/warp-releases/releases/latest) as a standalone binary.

## macOS

Using [brew](https://brew.sh/) is recommended:

```sh
$ brew install warpdl/tap/warpdl
$ warpdl --version
```

To update:
```sh
$ brew upgrade warpdl
```

Alternatively, you can install the CLI via [shell script](#shell-script), or via the warpdl `.pkg` file on the [Releases](https://github.com/warpdl/warp-releases/releases/latest) page. These methods will install the warpdl binary directly to `/usr/local/bin` and do not support seamless updates. To update, you'll need to re-run the installation.

## Windows

### Scoop

Using [scoop](https://scoop.sh/) is recommended:

```sh
$ scoop bucket add warpdl https://github.com/warpdl/scoop-bucket.git
$ scoop install warpdl
$ warpdl  --version
```

To update:

```sh
$ scoop update warpdl
```

### Git Bash

Using [Git Bash](https://git-scm.com/download/win) is also supported:

```sh
$ mkdir -p $HOME/bin
$ curl -Ls --tlsv1.2 --proto "=https" --retry 3 https://cli.warpdl.org/install.sh | sh -s -- --install-path $HOME/bin
$ warpdl --version
```

## Linux

### Alpine
Use the [Shell Script](#shell-script) installation method.

### Debian/Ubuntu (apt)

```bash
# install necessary packages
$ sudo apt-get update && sudo apt-get install ca-certificates curl gnupg -y

# add apt gpg key
$ curl -fsSL https://repo.warpdl.org/apt/gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/warpdl.gpg

# add apt repo
$ echo "deb [signed-by=/etc/apt/keyrings/warpdl.gpg] https://repo.warpdl.org/apt/ /" | sudo tee /etc/apt/sources.list.d/warpdl.list

# install latest warp package
$ sudo apt-get install warp

# (optional) print cli version
$ warpdl --version
```

To update:

```bash
$ sudo apt-get update && sudo apt-get upgrade warp
```

### RedHat/CentOS (yum)

```bash
# import gpg key
$ sudo rpm --import 'https://repo.warpdl.org/rpm/gpg.key'

# add yum config
$ curl -sLf --retry 3 --tlsv1.2 --proto "=https" 'https://raw.githubusercontent.com/warpdl/warp-releases/main/configs/rpm/config.rpm.txt' | sudo tee /etc/yum.repos.d/warpdl.repo

# install latest warp package
$ sudo yum update && sudo yum install warp

# (optional) print cli version
$ warpdl --version
```

To update:
```bash
$ sudo yum update warp
```

## Shell script

You can bypass package managers and quickly install the latest version of the CLI via shell script. The script automatically downloads and installs the CLI binary most appropriate for your system's architecture. It is also fully POSIX compliant to support all linux and bsd variants with minimal dependencies.

Note that this installation method is most recommended for ephemeral environments like CI jobs. Longer-lived environments that would like to receive updates via  package manager should install the CLI via that package manager.

```sh
(curl -Ls --tlsv1.2 --proto "=https" --retry 3 https://cli.warpdl.org/install.sh || wget -t 3 -qO- https://cli.warpdl.org/install.sh) | sh
```

You can find the source `install.sh` file in this repo's `scripts` directory.

## Docker

We currently publish a `ghcr.io/warpdl/warp-cli` Docker image based on `alpine`.


## Other

You can download all binaries and release artifacts from the [Releases](https://github.com/warpdl/warp-releases/releases/latest) page. Binaries are built for macOS, Linux, Windows, FreeBSD, OpenBSD, and NetBSD, and for 32-bit, 64-bit, armv6/armv7, and armv6/armv7 64-bit architectures.

You can also directly download the generated `.deb`, `.rpm`, and `.apk` packages. If a binary does not yet exist for the OS/architecture you use, please open a GitHub Issue.

# Verify Signature

You can verify the integrity and authenticity of any released artifact using a public GPG key. All release artifacts are signed and have a corresponding signature file. Release artifacts are available on the [Releases](https://github.com/warpdl/warp-releases/releases) page.

```sh
# fetch GPG signing key
gpg --keyserver keyserver.ubuntu.com --recv 9CAFFF2AC5F94C7C
# example: verify a release package
gpg --verify warp_0.0.27_linux_amd64.tar.gz.sig warp_0.0.27_linux_amd64.tar.gz || echo "Verification failed!"
```
