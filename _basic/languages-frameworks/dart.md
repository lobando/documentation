---
title: Using Dart In CI/CD with Codeship Basic
shortTitle: Dart
tags:
  - dart
  - languages
menus:
  basic/languages:
    title: Dart
    weight: 8
categories:
  - Languages And Frameworks
redirect_from:
  - /languages/dart/
---

* include a table of contents
{:toc}

## Versions And Setup

`$DART_SDK` is available in the Environment and included in the PATH. The installed version of the Dart SDK is `1.5.1`.

You can use these commands from the Dart SDK:

* Dart-to-JavaScript compiler (dart2js)
* Dart VM (dart)
* Dart package manager (pub)
* Dart Analyzer (dart_analyzer)

### Installing New Versions

To change to another version, use [this script](https://github.com/codeship/scripts/blob/master/languages/dart.sh) in your Setup Commands.

## Dependencies

You can install any dependencies you defined in your `pubspec.yaml` by running

```shell
pub get
```

### Dependency Cache

We do not cache Dart dependencies between builds by default, but any dependencies moved into the `$HOME/cache` directory before the end of the build will be cached and can be retrieved from that directory on the next build.

## Frameworks And Testing

As dart currently doesn't have a default way to run your tests you can use exactly the same command to run those tests as you would on your local machine. Note that almost all tools for custom machine configuration will install and run without issue on Codeship.

### Browser testing

We automatically have `xvfb` running on our System. You can use Firefox, Chrome
or PhantomJS to run your Dart tests in a browser. You can read more in our
[Browser Testing Guide]({{ site.baseurl }}{% link _basic/continuous-integration/browser-testing.md %})

## Parallel Testing

If you are running [parallel test pipelines]({{ site.baseurl }}{% link _basic/builds-and-configuration/parallel-tests.md %}), you will want separate your tests into groups and call a group specifically in each pipeline. For instance:

**Pipeline 1:**
```shell
pub run test tests/tests_1.dart
```

**Pipeline 2:**
```shell
pub run test tests/tests_2.dart
```

### Parallelization Modules

In addition to parallelizing your tests explicitly [via parallel pipelines]({{ site.baseurl }}{% link _basic/builds-and-configuration/parallel-tests.md %}), some customers have found using Dart test runner's built-in test parallelization is a good way to speed up your tests.

Note that aggressive parallelization can cause resource and build failure issues, as well.

## Notes And Known Issues

Due to Dart version and build issues, you may find it helpful to tests your commands with different versions via an [SSH debug session]({{ site.baseurl }}{% link _basic/builds-and-configuration/ssh-access.md %}) if tests are running differently on Codeship compared to your local machine.
