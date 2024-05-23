# libtatsu

Library handling the communication with Apple's Tatsu Signing Server (TSS).

![](https://github.com/libimobiledevice/libtatsu/workflows/build/badge.svg)

## Table of Contents
- [Features](#features)
- [Building](#building)
  - [Prerequisites](#prerequisites)
    - [Linux (Debian/Ubuntu based)](#linux-debianubuntu-based)
    - [macOS](#macos)
    - [Windows](#windows)
  - [Configuring the source tree](#configuring-the-source-tree)
  - [Building and installation](#building-and-installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [Links](#links)
- [License](#license)
- [Credits](#credits)

## Features

This library is part of the [libimobiledevice](https://github.com/libimobiledevice)
project. The main purpose of this library is to allow creating TSS request
payloads, sending them to Apple's TSS server, and retrieving and processing
the response.

The code was originally part of [idevicerestore](https://github.com/libimobiledevice/idevicerestore)
and has been split out to its own library, while obviously [idevicerestore](https://github.com/libimobiledevice/idevicerestore)
will remain the main consumer.

## Building

### Prerequisites

You need to have a working compiler (gcc/clang) and development environent
available. This project uses autotools for the build process, allowing to
have common build steps across different platforms.
Only the prerequisites differ and they are described in this section.

libtatsu requires [libplist](https://github.com/libimobiledevice/libplist)
**version 2.6.0** or later.
Check the [Building](https://github.com/libimobiledevice/libplist?tab=readme-ov-file#building)
section of the README on how to build it. Note that some platforms might have it as a package.
Also [libcurl](https://github.com/curl/curl) is required, but most platforms
already have it available as a package.

#### Linux (Debian/Ubuntu based)

* Install all required dependencies and build tools:
  ```shell
  sudo apt-get install \
  	build-essential \
  	pkg-config \
  	checkinstall \
  	git \
  	autoconf \
  	automake \
  	libtool-bin \
  	libplist-dev \
	libcurl4-openssl-dev
  ```

  In case libplist-dev is not available, you can manually build and install it. See note above.

#### macOS

* Make sure the Xcode command line tools are installed. Then, use either [MacPorts](https://www.macports.org/)
  or [Homebrew](https://brew.sh/) to install `automake`, `autoconf`, `libtool`, etc.

  Using MacPorts:
  ```shell
  sudo port install libtool autoconf automake pkgconfig
  ```

  Using Homebrew:
  ```shell
  brew install libtool autoconf automake pkg-config
  ```

  For libcurl, it is recommended to use the system specific library:
  ```shell
  export libcurl_CFLAGS="-I`xcrun --sdk macosx --show-sdk-path 2>/dev/null`/usr/include"
  export libcurl_LIBS="-lcurl"
  ```

#### Windows

* Using [MSYS2](https://www.msys2.org/) is the official way of compiling this project on Windows. Download the MSYS2 installer
  and follow the installation steps.

  It is recommended to use the _MSYS2 MinGW 64-bit_ shell. Run it and make sure the required dependencies are installed:

  ```shell
  pacman -S base-devel \
  	git \
  	mingw-w64-x86_64-gcc \
  	make \
  	libtool \
  	autoconf \
  	automake-wrapper \
  	pkg-config
  ```
  NOTE: You can use a different shell and different compiler according to your needs. Adapt the above command accordingly.

### Configuring the source tree

You can build the source code from a git checkout, or from a `.tar.bz2` release tarball from [Releases](https://github.com/libimobiledevice/libtatsu/releases).
Before we can build it, the source tree has to be configured for building. The steps depend on where you got the source from.

Since libtatsu depends on other packages, you should set the pkg-config environment variable `PKG_CONFIG_PATH`
accordingly. Make sure to use a path with the same prefix as the dependencies. If they are installed in `/usr/local` you would do

```shell
export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig
```

* **From git**

  If you haven't done already, clone the actual project repository and change into the directory.
  ```shell
  git clone https://github.com/libimobiledevice/libtatsu
  cd libtatsu
  ```

  Configure the source tree for building:
  ```shell
  ./autogen.sh
  ```

* **From release tarball (.tar.bz2)**

  When using an official [release tarball](https://github.com/libimobiledevice/libtatsu/releases) (`libtatsu-x.y.z.tar.bz2`)
  the procedure is slightly different.

  Extract the tarball:
  ```shell
  tar xjf libtatsu-x.y.z.tar.bz2
  cd libtatsu-x.y.z
  ```

  Configure the source tree for building:
  ```shell
  ./configure
  ```

Both `./configure` and `./autogen.sh` (which generates and calls `configure`) accept a few options, for example `--prefix` to allow
building for a different target folder. You can simply pass them like this:

```shell
./autogen.sh --prefix=/usr/local
```
or
```shell
./configure --prefix=/usr/local
```

Once the command is successful, the last few lines of output will look like this:
```
[...]
config.status: creating config.h
config.status: executing depfiles commands
config.status: executing libtool commands

Configuration for libtatsu 1.0.0:
-------------------------------------------

  Install prefix: .........: /usr/local

  Now type 'make' to build libtatsu 1.0.0,
  and then 'make install' for installation.
```

### Building and installation

If you followed all the steps successfully, and `autogen.sh` or `configure` did not print any errors,
you are ready to build the project. This is simply done with

```shell
make
```

If no errors are emitted you are ready for installation. Depending on whether
the current user has permissions to write to the destination directory or not,
you would either run
```shell
make install
```
_OR_
```shell
sudo make install
```

If you are on Linux, you want to run `sudo ldconfig` after installation to
make sure the installed libraries are made available.

## Usage

This library is directly used by idevicerestore and libimobiledevice, so there
is no need to do anything in particular. Feel free to use it in your project,
check the header files for available functions. A documentation might be added
later.

## Contributing

We welcome contributions from anyone and are grateful for every pull request!

If you'd like to contribute, please fork the `master` branch, change, commit and
send a pull request for review. Once approved it can be merged into the main
code base.

If you plan to contribute larger changes or a major refactoring, please create a
ticket first to discuss the idea upfront to ensure less effort for everyone.

Please make sure your contribution adheres to:
* Try to follow the code style of the project
* Commit messages should describe the change well without being too short
* Try to split larger changes into individual commits of a common domain

## Links

* Homepage: https://libimobiledevice.org/
* Repository: https://github.com/libimobiledevice/libtatsu.git
* Issue Tracker: https://github.com/libimobiledevice/libtatsu/issues
* Mailing List: https://lists.libimobiledevice.org/mailman/listinfo/libimobiledevice-devel
* Twitter: https://twitter.com/libimobiledev

## License

This library is licensed under the [GNU Lesser General Public License v2.1](https://www.gnu.org/licenses/lgpl-2.1.en.html),
also included in the repository in the `COPYING` file.

## Credits

Apple, iPhone, iPad, iPod, iPod Touch, Apple TV, Apple Watch, Mac, iOS,
iPadOS, tvOS, watchOS, and macOS are trademarks of Apple Inc.

This project is an independent software library and has not been authorized,
sponsored, or otherwise approved by Apple Inc.

README Updated on: 2024-05-19

