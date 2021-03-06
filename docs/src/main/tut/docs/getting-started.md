---
layout: docs
title: Getting Started
section: docs
weight : 1
---

# Prerequisites

* [sbt](http://www.scala-sbt.org/) 0.13.8+
* [jekyll](https://jekyllrb.com/)

To satisfy the `jekyll` prerequisite, here are a few hints for local and travis environments.

## Local Environment

Depending on your platform, you might do this with:

```bash
yum install jekyll

apt-get install jekyll

gem install jekyll
```

## Continuous Integration - Travis

If you have enabled [Travis](https://travis-ci.org/) for your project, you might have to tweak some parts of your `.travis.yml` file:

Potentially, your project is a Scala project (`language: scala`), therefore you need to add the bundle gems vendor path in the `PATH` environment variable:

```
before_install:
 - export PATH=${PATH}:./vendor/bundle
```

This is needed in order to install and be able to use the `jekyll` gem from other parts of your travis descriptor file. Once we have the `/vendor/bundle` path in the Travis `PATH` env variable, we have to install the gem in the `install` travis section:

```
install:
 - ...
 - gem install jekyll -v 2.5
```

# Set it up in your Project

To Begin, add the following lines to the `project/plugins.sbt` file within your project or sbt module where you want to use the `sbt-microsites` plugin. Depending on the version, you might want to use:

Latest release:

```
addSbtPlugin("com.fortysevendeg"  % "sbt-microsites" % "0.2.0")
```

Latest snapshot built from the `master` branch code:

```tut:evaluated
println("""resolvers += Resolver.sonatypeRepo("snapshots")""")
println(s"""addSbtPlugin("com.fortysevendeg"  % "sbt-microsites" % "${microsites.BuildInfo.version}"""")
```

Finally, to enable the plugin, add this to your `build.sbt` file:
```
enablePlugins(MicrositesPlugin)
```
