librecore-utils
===============

ABOUT
=====

The ```librecore-utils``` project contains all the supporting
userland components for both developers and users alike.

Typically these tools either provide diagnostic telemetry of
board bring-up or provide mechanisms to extract useful
hardware specific details within the porting process to a
new target.

BUILD
=====

You make compile out of tree in the following way:

```
 $ mkdir build && cd build/
 $ cmake ../
 $ make
```

further, the build system will generate typical distribution
packages for easy of installation on your system as follows:

```
 $ make package
```

Kindly,
 ~ librecore team ::.
