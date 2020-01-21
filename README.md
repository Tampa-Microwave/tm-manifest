# Tampa Microwave Yocto (Timmy!) Manifest

This repository contains the manifest files for Tampa Microwaves' Yocto distribution. It is a fork of Digi Embedded's Yocto distribution and their entire README is included at the end of this document.

## Installation

### QUICK

If you're on a new machine, the following command will install system dependencies, download the sources, and setup an initial build directory. You'll need your `sudo` password and any ssh keys required for accessing Tampa Microwave private GitHub repositories.

```shell
bash <(curl -fsSL https://raw.githubusercontent.com/sr105-tm/tm-manifest/thud/bootstrap.sh)
```

### Google repo tool

Download Google's repo tool to a directory within your path and add execution
permissions. Repo is a tool for downloading many different source repositories
and arranging them locally. All of the details are defined in an XML manifest
file found in its own repo, this one.

```shell
sudo curl -o /usr/local/bin/repo http://commondatastorage.googleapis.com/git-repo-downloads/repo
sudo chmod a+x /usr/local/bin/repo
```

### Download the manifest sources

Use the repo tool to download and install of the sources needed for our
distribution. The default manifest file is set to perform shallow clones of
upstream sources to save space. Choose a single, semi-permanent place to
download the sources. You'll do your builds in (optionally) separate build
directories.

```shell
mkdir -p /path/to/tm-2.6
cd /path/to/tm-2.6
repo init -u https://github.com/sr105-tm/tm-manifest -b thud
repo sync
```

### Create a Build Directory

Now, create an initial build directory as detailed in the README file in the
root level of the downloaded sources. It is reproduced here:

```shell
mkdir -p /path/to/build
cd /path/to/build
. /path/to/tm-2.6/sources/meta-tm-sw/conf/tm-env
```

This will create a symbolic link to the `tm-env` file and initialize a build
configuration in your new build directory.

### Build an Image

You will need to source the `tm-env` file anytime you open a new terminal.

```shell
. /path/to/build/tm-env
# You are now inside /path/to/build and the environment is initialized for
# building.
bitbake tm-image
```

This will take about 3 hours for the first build. Future builds will only build
changes. If all goes well, the output is in `/path/to/build/tmp/deploy/images`.


Digi Embedded Yocto (DEY) manifest
==================================

This repository contains the manifest files for the Digi Embedded Yocto
distribution for [Digi's Embedded modules](https://www.digi.com/products/embedded-systems).

Installing Digi Embedded Yocto
------------------------------

To download Digi Embedded Yocto, you need the repo tool.

Follow these steps to install Digi Embedded Yocto:

1. Download repo to a directory within your path and add execution permissions.

    ```
    $ sudo curl -o /usr/local/bin/repo http://commondatastorage.googleapis.com/git-repo-downloads/repo
    $ sudo chmod a+x /usr/local/bin/repo
    ```

2. Create an installation folder with user write permissions; for example,
    `/usr/local/dey-2.6` and navigate to that folder.

    ```
    $ sudo install -o <your-user> -g <your-group> -d /usr/local/dey-2.6
    $ cd /usr/local/dey-2.6
    ```

    Note: You can get your primary user and group using the `id` command.

3. Use repo to download Digi Embedded Yocto.

    ```
    $ repo init -u https://github.com/digi-embedded/dey-manifest.git -b thud
    $ repo sync -j8 --no-repo-verify
    ```

More information about [Digi Embedded Yocto](https://github.com/digi-embedded/meta-digi).

License
-------
Copyright 2019, Digi International Inc.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
