# Godot C++ CMaker

## Initialization

```shell
git init
git submodule add git@github.com:yehuthi/godot_cpp_cmaker.git
git submodule update --init --recursive
```

In your `CMakeLists.txt` add the subdirectory create your library target as shared, and use the provided CMake function `gdextension`, e.g.:
```cmake
add_library(my_gdextension SHARED ${SOURCES})
#                          ^^^^^^

# ...

add_subdirectory(godot_cpp_cmaker)
gdextension(my_gdextension)
```

## Output

It's common practice to have the Godot game project in a directory inside the GDExtension project. It's assumed that this directory would be called "game", and if it exists, the artifacts will be built into "game/bin". Otherwise, into the the CMake build directory under the "bin" directory.