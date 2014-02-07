sbtg
====

A tiny Ruby tool to make sbt and growl work together effectively.

Totally inspired by and originally started as a fork of https://github.com/tommorris/sbt-growltest

At the time of this writing, the project mentioned above had not been updated in four years and sbtg has now developed into something quite different, so I decided that it cannot be a fork any longer but needs its own project.

One reason why I chose to build this wrapper rather than using an existing sbt plugin (https://github.com/softprops/sbt-growl-plugin) is the fact that the plugin simply does not work for me (OS X 10.9.1, growl 2.1.3, sbt 0.13.1, scala 2.10.3).

I may come back to reviewing the sbt plugin in the future, but for now, using Ruby helped me to get productive with sbt and growl very quickly. It also sports a few nice extra features (see below).


Prerequistes
============

You will need to have

1. Ruby (will work with MRI 1.8.7, 1.9.3 and 2.0.0)
2. Growl and growlnotify, which makes this solution a Mac-only thing
3. Obvioulsy: sbt (tested with 0.13.x and 0.12.x)


Installation
============

1. Clone the repo
2. Create a symlink to the sbtg script that you will find in the cloned repo from whichever directory you prefer to store executable scripts in (for example in ~/bin). Obvioulsy, it makes sense for this directory to be contained in your $PATH.

Supported SBT versions
======================

sbtg currently supports versions 0.12.x and 0.13.x. There is one difference between these two which the script handles: testOnly vs. test-only are the respective task names.
sbtg reads the sbt version from ```project/build.properties```. The value found in there can be overriden with a shell / environment variable, eg like so:
```
$SBT_VERSION=0.12 sbtg ...`

Usage / Features
================

Here's what you can now do, always assuming that you first cd into the scala project's root:

## sbt ~ test
In order to run ```sbt '~ test'``` and have it do red / green notification via growl, simply type

```
$ sbtg
```

The wrapper will look at the console log produced by sbt and notify accordingly. You can concentrate on your IDE / Editor and do not have to switch to a terminal to see if you just broke a test.

## sbt ~ testOnly
Say you have a scala project with these tests:

<pre>
./src/test/scala/conway/GameSpec.scala
./src/test/scala/conway/OscillatorsSpec.scala
./src/test/scala/conway/RulesSpec.scala
./src/test/scala/conway/SpaceshipsSpec.scala
</pre>

And you want to run the RulesSpec test continuously in the background while hacking away in your IDE / Editor. You can achieve this conveniently by typing

```
$ sbtg Rule
```

The wrapper will translate this into

```
$ sbt '~ testOnly conway.RulesSpec'
```

It can do this by looking at the names of all tests it finds recursively in ```./src/test/scala``` and then figuring out that only the test ```conway.RulesSpec``` matches your input.

## sbt ~ testOnly: Interactive selection of test
If you specify a test name fragment that resolves to more than one test, you will be presented with a selection as shown below:

<pre>
$ sbtg Spec
Your input ["Spec"] is ambiguous. Please select from these candidates:
0 - conway.GameSpec
1 - conway.OscillatorsSpec
2 - conway.RulesSpec
3 - conway.SpaceshipsSpec
</pre>

You can now continue by selecting the test that you originally had in mind but were too lazy to fully specify. Convenience rules!

These features add value in my view: I do not have to remember and type the complete name and package in which a test resides in order to run it continuously in the background.

Next
====

- Output more information on failure (eg name of first failed test)

Finally: Your bug reports, general feedback as well as Feature- and Pull Requests are welcome!

