# ImGui as a Library

CMake cross platform module for building [Dear ImGui](https://github.com/ocornut/imgui) as a library.


## Getting Started

```bash
git clone --recursive https://github.com/GrabCAD/imgui-cmake
cd ImGui-CMake-Installer && mkdir build && cd build
cmake .. -DIMGUI_WITH_IMPL=OFF
cmake --build . --config Release --target install
```

By default it would build ImGui as a static library, but if you would like to build as a shared library(DLL), turn off `IMGUI_STATIC_LIBRARY` option when generating the project:
```bash
cmake .. -DIMGUI_WITH_IMPL=OFF -DIMGUI_STATIC_LIBRARY=OFF
```

Notice that cmake will automatically use the lastest visual studio installed on your computer.
If you would like to change the visual studio version used for compilation use one of the [following options](https://cmake.org/cmake/help/latest/manual/cmake-generators.7.html).
here is a simple example on how to compile with visual studio 2017 for 64bit version:
```bash
cmake .. -G "Visual Studio 15 2017 Win64"
```

There are few things you want to know when you build `Dear ImGui`:<br>
ImGui comes with examples that already takes care of the way people should interact with the library, i.e `imgui_impl_win32.cpp`, `imgui_impl_vulkan.cpp`, `imgui_impl_osx.mm` `imgui_impl_sdl.cpp` etc...
If you want to include one of the examples in the library build, when you generate the cmake project, you'll want to pass which graphic API you want to include in your build. Example:
```bash
cmake .. -DIMGUI_IMPL_DX11=ON
```

That would basically copy and include in your library build the following files:<br>
`imgui_impl_win32.cpp` `imgui_impl_win32.h`, `imgui_impl_dx11.cpp`, `imgui_impl_dx11.h`
and the headers will also be copied under `dist/include` directory.

### Nuget Update

This project was originally made for ease of imgui nuget update, as it allows fast creation of binary artifacts for various compiler configurations.
here is an example on how to build debug and release artifacts for visual studion 2017 and visual studio 2013 in one script:
```bash
git clone --recursive https://github.com/GrabCAD/imgui-cmake

cd ImGui-CMake-Installer && mkdir build2017 && cd build2017
cmake .. -DIMGUI_WITH_IMPL=OFF -DIMGUI_STATIC_LIBRARY=OFF
cmake .. -G "Visual Studio 15 2017 Win64"
cmake --build . --config Release --target install
cmake --build . --config Debug --target install

cd.. && mkdir build2013 && cd build2013
cmake .. -G "Visual Studio 12 2013 Win64"
cmake --build . --config Release --target install
cmake --build . --config Debug --target install
```


