---
layout: post
title: How to install HHVM on Debian Stretch
slug: libvpx1-hhvm-debian-stretch
category: System
tags: debian stretch package hhvm
published: true
summary: How to install HHVM on Debian Stretch
---

After reading the reply from the HHVM maintainers on [Debian jessie package 
doesn't work on Debian stretch](https://github.com/facebook/hhvm/issues/5464),
I decided to solve the problem myself.

## TL;DR: Give me the package

Sure, download the precompiled package (for x64 only).

[libvpx1_1.3.0-3_amd64.deb](/upload/libvpx1_1.3.0-3_amd64.deb)


## I want to compile it myself

#### 1. Compile libvpx1 from source

This turned out to be pretty easy. I downloaded the libvpx1 [source
package](https://packages.debian.org/jessie/libvpx1) for Jessie from
Debian and compiled it. The first time I ran into an error because the libvpx1
source code uses a typedef already defined in `stddef.h`. A quick patch and
recompile and the package was ready to be installed.
The patch involves renaming the typedef on line 33 in the files
`nestegg/halloc/src/align.h` and `nestegg/halloc/src/halloc.c`. By a freakish
accident, it's the same line number.

`$ dpkg-source -x libvpx_1.3.0-3.dsc`

`$ cd libvpx-1.3.0`

`$ debuild -us -uc -b`

#### 2. Install the newly created libvpx1 package

`$ sudo dpkg -i libvpx1_1.3.0-3_amd64.deb`

#### 3. Install hhvm (or any other package requiring libvpx1)

`$ sudo apt-get install hhvm`

-------------------

If you found this post helpful or have a question, leave a comment or get in
touch.
