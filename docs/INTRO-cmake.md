
# Introduction to SDL_ttf with CMake

The easiest way to use SDL_ttf is to include it along with SDL as subprojects in your project.

We'll start by creating a simple project to build and run [hello.c](hello.c)

Create the file CMakeLists.txt
```cmake
cmake_minimum_required(VERSION 3.16)
project(hello)

# set the output directory for built objects.
# This makes sure that the dynamic library goes into the build directory automatically.
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/$<CONFIGURATION>")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/$<CONFIGURATION>")

# Use vendored libs
set(SDLTTF_VENDORED ON)

# This assumes the SDL source is available in vendored/SDL
add_subdirectory(vendored/SDL EXCLUDE_FROM_ALL)

# This assumes the SDL_ttf source is available in vendored/SDL_ttf
add_subdirectory(vendored/SDL_ttf EXCLUDE_FROM_ALL)

# Create your game executable target as usual
add_executable(hello WIN32 hello.c)

# Link to the actual SDL3 library.
target_link_libraries(hello PRIVATE SDL3_ttf::SDL3_ttf SDL3::SDL3)
```
Run [external/download.sh](../external/download.sh) or [external/Get-GitModules.ps1](../external/Get-GitModules.ps1)


Build:
```sh
cmake -S . -B build
cmake --build build
```

Run:
- On Windows the executable is in the build Debug directory:
```sh
cd build/Debug
./hello
``` 
- On other platforms the executable is in the build directory:
```sh
cd build
./hello
```

A more complete example is available at:

https://github.com/Ravbug/sdl3-sample

