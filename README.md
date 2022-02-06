# PySide2 whl for Nvidia Jetson

Compiled PySide2 for Qt 5.12 on ARM system (exp. on Nvidia Jetson Nano). Tested on Ubuntu 20.04 (upgraded Ubuntu 18.04 JetPack 4) with Python 3.6(m).

## Installation

To install PySide2 + shiboken2 execute the command:

    pip3 install *.whl
  
## Dependences and requirements

This wheel package is only for aarch64 systems.

Also, the machine needs to have Qt 5.12 on board, Python3... it's not done yet - I didn't tested it on old linux and other systems, but it have to work with Python 3.6 and Ubuntu 20.04+.
