---
layout: single
title: Unit Testing With C++
categories:
    - C++
tags:
    - bazel
excerpt: Bazel build engine for c++
comments: true
---
For last couple of months I am in love with writing `Unit Tests`. I wasn't like that. You may say I was adventurous, hardcore and love living dangerous life! But that wasn't the case, believe me. I was just plain dumb. So how was my life before I started writing `Unit Tests`?

I was so afraid to refactor my codes. There is a high possibility it may break something else in somewhere that I will not be able to detect soon. But eventually when I will do, it will be very hard to trace why it is broken and fix it. Nobody around me told me to write `Unit Tests` and few who did, didn't even write `Unit Tests` when they code! It was like [Aesob](https://en.wikipedia.org/wiki/Aesop)'s [The Two Crabs](https://fablesofaesop.com/the-two-crabs.html) story I read at my childhood. It was a mess.

{% responsive_image path: assets/images/the-two-crab-aesop.jpg %}


> Build and test software of any size, quickly and reliably

Contet of `WORKSPACE` file -
```
new_git_repository(
    name = "googletest",
    build_file = "gmock.BUILD",
    remote = "https://github.com/google/googletest",
    tag = "release-1.8.0",
)
```

and the content fo `gmock.BUILD` file is -

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

The content of the -
```cpp
#include "gtest/gtest.h"

#include "MyLib/message.hpp"

TEST(message_test,content)
{
  EXPECT_EQ(get_message(),"Hello World!");
}

TEST(myonw_test_testing, content)
{
  EXPECT_EQ(4, 2+4);
}

TEST(another_test, content)
{
  EXPECT_EQ(6, 3*4);
}
```