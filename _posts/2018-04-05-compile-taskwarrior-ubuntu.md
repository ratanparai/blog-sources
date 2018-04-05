---
layout: single
title: Compile TaskWarrior in Ubuntu
date: 2018-04-05 21:50:00 +0600
categories:
    - Taskwarrior
excerpt: Although you can install `TaskWarrior` from `Ubuntu` package manager, but it doesn't have latest version. So you have to download source code and compile it.
tags:
    - Ubuntu
---

[Taskwarrior](https://taskwarrior.org/) is Free and Open Source Software that manages your TODO list from the command line. It is flexible, fast, and unobtrusive. It does its job then gets out of your way.

Although you can install `TaskWarrior` from `Ubuntu` package manager, but it doesn't have latest version. So to get the latest version of `TaskWarrior`, you have to download source code and compile it.

Install required package in ubuntu

```bash
$ sudo apt install -y build-essential cmake git uuid-dev libgnutls28-dev
```


download taskwarrior archive

```bash
$ wget [url_of_latest_task-x.x.x.tar.gz]
```

After installing required packages run those following command to build and install taskwarrior on your machine


```bash
$ ls
$ task-x.x.x.tar.gz
$ tar xzvf task-x.x.x.tar.gz
$ cd task-x.x.x
$ cmake -DCMAKE_BUILD_TYPE=release .
...
$ make
...
$ sudo make install
```

Change the `x's` with the correct version number from the [TaskWarrior Download](https://taskwarrior.org/download/) page.

Now run `Taskwarrior` from terminal by the command -

```bash
$ task
```
