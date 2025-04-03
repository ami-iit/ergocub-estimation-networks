# ergocub-estimation-networks

This repository hosts data-driven models (so-called "neural networks") in ONNX format used for estimation tasks on ergoCub robots.

They are meant to be consumed by software contained on [`bipedal-locomotion-framework`](https://github.com/ami-iit/bipedal-locomotion-framework/).

## Maintainers

This repository is maintained by:

* Ines Sorrentino ([@isorrentino](https://github.com/isorrentino))

## Installation

### Dependencies

Make sure you have available the following resources:
- [CMake](https://cmake.org/)


### Install

From the repository root level do:
```console
cmake -S . -B build
cmake --build build/ --target install
```

As result, the configurations files of your own robot should be placed in `$CMAKE_INSTALL_PREFIX/share/ICUBcontrib/robots/$YARP_ROBOT_NAME`, that is the same location used by the [`robots-configuration`](https://github.com/robotology/robots-configuration) repository already used to store ergoCub software configurations.
