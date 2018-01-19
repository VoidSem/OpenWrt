# Make Ubuntu EVM

## Clone Repo

```
git clone git://git.openwrt.org/openwrt.git
cd openwrt
./scripts/feeds update -a
./scripts/feeds install -a
```

## Install Package

```
sudo apt-get install g++
sudo apt-get install libncurses5-dev
sudo apt-get install zlib1g-dev
sudo apt-get install bison
sudo apt-get install flex
sudo apt-get install unzip
sudo apt-get install autoconf
sudo apt-get install gawk
sudo apt-get install make
sudo apt-get install gettext
sudo apt-get install gcc
sudo apt-get install binutils
sudo apt-get install patch
sudo apt-get install bzip2
sudo apt-get install libz-dev
sudo apt-get install asciidoc
sudo apt-get install subversion
sudo apt-get install sphinxsearch
sudo apt-get install libtool
sudo apt-get install sphinx-common
sudo apt-get install libssl-dev
sudo apt-get install libssl0.9.8
sudo apt-get install git-core
sudo apt-get install build-essential
sudo apt-get install mercurial
sudo apt-get install libssl-dev libncurses5-dev unzip
sudo apt-get install subversion mercurial
```

## make menuconfig

**Select i.MX6 for Test**

```
zengjf@desk-ubuntu:~/openwrt-17.01.4$ make menuconfig
Checking 'working-make'... ok.
Checking 'case-sensitive-fs'... ok.
Checking 'proper-umask'... ok.
Checking 'gcc'... ok.
Checking 'working-gcc'... ok.
Checking 'g++'... ok.
Checking 'working-g++'... ok.
Checking 'ncurses'... ok.
Checking 'zlib'... ok.
Checking 'perl-thread-queue'... ok.
Checking 'tar'... ok.
Checking 'find'... ok.
Checking 'bash'... ok.
Checking 'patch'... ok.
Checking 'diff'... ok.
Checking 'cp'... ok.
Checking 'seq'... ok.
Checking 'awk'... ok.
Checking 'grep'... ok.
Checking 'getopt'... ok.
Checking 'stat'... ok.
Checking 'unzip'... ok.
Checking 'bzip2'... ok.
Checking 'wget'... ok.
Checking 'perl'... ok.
Checking 'python'... ok.
Checking 'git'... ok.
Checking 'file'... ok.
Checking 'ldconfig-stub'... ok.
Collecting package info: done
Collecting target info: done
configuration written to .config

*** End of the configuration.
*** Execute 'make' to start the build or try 'make help'.
```
