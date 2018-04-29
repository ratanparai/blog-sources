---
layout: single
title: Writing unit tests for C++ with Bazel and GoogleTest
date: 2018-04-29 03:05:00 +0600
categories:
    - C++
tags:
    - bazel
    - googletest
excerpt: On my journey to be a better programmer, I stated to learn C++. This is how I am using bazel to build my project with google test integration.
comments: true
---
For last couple of months I am in love with writing **Unit Tests**. I wasn't like that. You may say I was adventurous, hardcore and love living dangerous life! But that wasn't the case, believe me. I was just plain dumb. So how was my life before I started writing **Unit Tests**?

I was so afraid to refactor my codes. There is a high possibility it may break something else in somewhere that I will not be able to detect soon. But eventually when I will do, it will be very hard to trace why it is broken and fix it. Nobody around me told me to write **Unit Tests** and few who did, didn't even write Unit Tests for themselves! It was like [Aesob](https://en.wikipedia.org/wiki/Aesop)'s [The Two Crabs](https://fablesofaesop.com/the-two-crabs.html) story I read at my childhood.

{% responsive_image path: assets/images/the-two-crab-aesop.jpg %}


Although I did some **C++** codes in University and attended some **Programming Competition** where I've used C++ for writing code, but I never did **Object Oriented Programming** with C++. So few months ago I have started learning C++ in my free time. At first I tried to use **CMAKE** to build. After using it for sometime, I found **Bazel**. It is faster, more organized and modular.

At first lets look at the folder structure-

```
│   gmock.BUILD
│   WORKSPACE
│
├───src
│   ├───lib
│   │       BUILD
│   │       Greeting.cc
│   │       Greeting.h
│   │
│   └───main
│           BUILD
│           main.cc
│
└───tests
        BUILD
        Greeting_test.cc
```

There should be a `WORKSPACE` file in the **root** of your source code. It contains **external dependencies**. If you don't have any external dependencies in your project, your `WORKSPACE` file should be empty, But you must have this file.

We are using **GoogleTest** as external dependency. Lets look inside our `WORKSPACE` file-

```
new_git_repository(
    name = "googletest",
    build_file = "gmock.BUILD",
    remote = "https://github.com/google/googletest",
    tag = "release-1.8.0",
)
```

Here, the dependency is added as a git repository. As a result, when we build the project, it will download the **git** repository and run the `build_file` **gmock.BUILD** to build the **GoogleTest** library, which we will import in our **tests**. The content of the **gmock.BUILD** file is-

```
cc_library(
    name = "gtest",
    srcs = [
        "googletest/src/gtest-all.cc",
        "googlemock/src/gmock-all.cc",
    ],
    hdrs = glob([
        "**/*.h",
        "googletest/src/*.cc",
        "googlemock/src/*.cc",
    ]),
    includes = [
        "googlemock",
        "googletest",
        "googletest/include",
        "googlemock/include",
    ],
    linkopts = ["-pthread"],
    visibility = ["//visibility:public"],
)

cc_library(
    name = "gtest_main",
    srcs = ["googlemock/src/gmock_main.cc"],
    linkopts = ["-pthread"],
    visibility = ["//visibility:public"],
    deps = [":gtest"],
)
```

This concludes our initial setup of **GoogleTest** with **Bazel**. Now we need to add `@googletest//:gtest_main` as a dependency of our test library, `cc_test` and import `gtest/gtest.h` to our **unit test** file. Example **BUILD** file `tests` -

```
cc_test(
    name = "tests",
    srcs = glob(["**/*.cc"]),
    deps = [
        "//src/lib:GreetingLib",
        "@googletest//:gtest_main",
    ],
)
```

> Here the first dependency is `cc_library` dependency, where we have a `Greeting` class that have a **public** method, `getGreetingMessage()` that return `Hello World!`.

And content of the `greeting_test.cc`-
```cpp
#include "gtest/gtest.h"
#include "src/lib/Greeting.h"

TEST(GreetingShould, ReturnHelloWorld){
    Greeting *greet = new Greeting();
    std::string actual = greet->getGreetingMessage();
    std::string expected = "Hello World!";
    EXPECT_EQ(expected, actual);
}
```

### Building and Running unit tests
Building the gradle project is easy. You just need to run-

```bash
$ bazel build ...
```

to build every **cc_library** and **cc_binary** of the project. And to run all **unit tests** just run-

```bash
$ bazel test ...
```

I have created a **git** repository , which you can clone and use as your starting point. Please feel free to **star** it if you think my repository helps you.

[CPP-Template](https://github.com/ratanparai/cpp-template)