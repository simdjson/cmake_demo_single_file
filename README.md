# cmake_demo_single_file


Really simple CMake demo using FetchContent

If you have a recent version of CMake (3.15 or better) under linux, macOS or freeBSD,  you can simply
go in the directory and type the following commands:

```
cmake -B build .
cmake --build build
./build/repro
```


The instructions with Visual Studio (Windows) are similar:


```
cmake -B build .
cmake --build build --config Release
./build/Release/repro.exe
```

## Getting CMake


1. On macOS, the easiest way to install cmake might be to use [brew](https://brew.sh) and then type
```
brew install cmake
```
2. Under Linux, you might be able to install CMake as follows:
```
apt-get update -qq
apt-get install -y cmake
```
3. On FreeBSD, you might be able to install bash and CMake as follows:
```
pkg update -f
pkg install bash
pkg install cmake
```

4. Under Windows, you may want to install [CMake](https://cmake.org/download/) using an installer.


## Using submodules

[You can also use simdjson as a submodule-based dependency.](https://github.com/simdjson/cmakedemo)
