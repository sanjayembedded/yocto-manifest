# Yocto Repo Manifest README

This repo is used to download manifests for Yocto releases.

Note that this does not include the Yocto Project's Poky repository. Instead, the import pieces that go into the poky repository are included from their upstream git repositories directly (e.g. oe-core, bitbake, etc).

This repo manifest exists to make it easier to submit changes to the base repositories of OpenEmbedded/Yocto as required by the poky documentation.


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
$: repo init -u https://github.com/sanjayembedded/yocto-manifest -b dunfell
$: repo sync
```
