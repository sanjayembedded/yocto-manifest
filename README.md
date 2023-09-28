# Yocto Repo Manifest README

This repo downloads manifests for Yocto releases.

Note that this does not include the Yocto Project's Poky repository. Instead, the import pieces that go into the Poky repository are included from their upstream git repositories directly (e.g. oe-core, bitbake, etc).

This repo manifest exists to make it easier to submit changes to the base repositories of OpenEmbedded/Yocto as required by the Poky documentation.


# Getting Started

## Install Google's repo utility:

Install the repo tool to use this manifest repo.
```
$: mkdir ~/bin
$: curl http://commondatastorage.googleapis.com/git-repo-downloads/repo  > ~/bin/repo
$: chmod a+x ~/bin/repo
$: PATH=${PATH}:~/bin
```

## Initialize a Repo client:

```
$: cd ${HOME}/${WORK_DIR}
$: mkdir <release>
$: cd <release>
$: repo init -u https://github.com/sanjayembedded/yocto-manifest -b <branch_name> [ -m <release manifest>]
$: repo sync
```

## Setup the build folder for a BSP release:

```
$: [MACHINE=<machine>] [DISTRO=<poky>] source source/openembedded-core/oe-init-build-env build
```

## Build an image:

```
$: bitbake <image recipe>
```

## Example:

```
$: repo init -u https://github.com/sanjayembedded/yocto-manifest -b master
$: repo sync
$: source source/openembedded-core/oe-init-build-env build
$: bitbake core-image-minimal
```

# Quick automation tool for SDK setup
Download [yocto-setup.sh](https://github.com/sanjayembedded/scripts/blob/master/yocto-setup.sh) and execute following command in Linux terminal:
```
source yocto-setup.sh <branch_name>
```

# Additional Information

## Optimize build time:
Add [DL_DIR](https://docs.yoctoproject.org/ref-manual/variables.html#term-DL_DIR) and [SSTATE_DIR](https://docs.yoctoproject.org/ref-manual/variables.html#term-SSTATE_DIR) configurations to conf/local.conf with a respective PATH variable.

```
DL_DIR = "${PATH_TO_DOWNLOADS}/"
SSTATE_DIR = "${PATH_TO_SSTATE_CACHE}/"
```

## Enabling [CVE](https://en.wikipedia.org/wiki/Common_Vulnerabilities_and_Exposures) check:

The Yocto Project provides a [cve-check class](https://github.com/openembedded/openembedded-core/blob/master/meta/classes/cve-check.bbclass) which can be enabled to scan packages for public CVE’s. You can use this feature to scan individual packages but also on images (which will scan all packages included in that specific image).

It utilizes the [NATIONAL VULNERABILITY DATABASE](https://nvd.nist.gov/), from which it performs the lookup.

To enable the CVE check you can add the following configuration to conf/local.conf:
> INHERIT += "cve-check"

Once this is enabled you can run CVE checks on individual package(s):
> bitbake -c cve_check <package/image name>

### Example:

```
$: bitbake -c cve_check openssl
$: bitbake core-image-sato
$: bitbake -k -c cve_check universe
```
