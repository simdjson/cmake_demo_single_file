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
./build/release/repro.exe
```


## Using submodules

[You can also use simdjson as a submodule-based dependency.](https://github.com/simdjson/cmakedemo)
