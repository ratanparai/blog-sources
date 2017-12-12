---
layout: single
title: Bazel build for c++
date: 2017-12-06 9:32:00 +0600
categories:
    - C++
tags:
    - bazel
excerpt: Bazel build engine for c++
comments: true
---
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