sbtg
====

Totally inspired by and originally a fork of https://github.com/tommorris/sbt-growltest

Now extended to also accomodate for specs/specs2 and adjusted to work with scalatest 2 and sbt 0.13.x

One reason why I chose to use this wrapper instead of an existing sbt plugin is the fact that the plugin simply does not work for me (OS X 10.9.1, growl 2.1.3, sbt 0.13.1, scala 2.10.3).

I may decide to fix the sbt plugin but using Ruby for now helped me get productive much quicker.

Usage
=====

Clone the repo. Then create a symlink to the sbtg script in whatever directory you usually put binaries/scripts in, eg ~/bin

You will need to have Ruby installed of course and this solution is Mac only.


Next
====

- Cater for ~ testOnly
- Output more information on failure (eg name of first failed test)
