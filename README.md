Basic Modern OpenGL App (Core Profile) with wxWidgets as the UI Framework to provide native OS controls for Mac, Windows, and Linux.

[![Video](/output.gif)](https://www.youtube.com/watch?v=P240ZPGK6HI)

Full Tutorial: https://www.youtube.com/watch?v=P240ZPGK6HI

## How this works

This template searches for the wxWidgets library using `FindPackage`. If not found, it downloads the library source from GitHub, compiles it, and links it with the main project. 

The super build pattern with `ExternalProject_Add` is used to achieve this.

## Requirements

This works on Windows, Mac, and Linux. You'll need `cmake` and a C++ compiler (tested on `clang`, `gcc`, and MSVC).

Linux builds require the GTK3 library and headers installed in the system.

## Building

To build the project, use:

```bash
cmake -S. -Bbuild
cmake --build build
```

This will create a directory named `build` and create all build artifacts there. The main executable can be found in the `build/subprojects/Build/wx_opengl_tutorial_core` folder.

---
Check out the blog for more! [www.lukesdevtutorials.com](https://www.lukesdevtutorials.com)
---

