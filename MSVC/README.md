[中文](README_CN.md)

Assuming that using Windows platform, VSCode and installing MSVC via VS Build Tool.

On Windows, you can find that if the library you need can be installed using MSYS2 or vcpkg.

This time I don't want to configure .vscode floder, so we will use CMake, a compile tool which can cross compiler and platform.

# 1. C++

Read this article:

[C/C++ for Visual Studio Code](https://code.visualstudio.com/docs/languages/cpp)

After setup, you can open the root folder of this project in VSCode, and run `hello_world.cpp`, choose cl.exe. 

Note that you should open VSCode via Developer Command Prompt. A .bat file can be helpful:

```batch
@echo off

call "C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools\Common7\Tools\VsDevCmd.bat"

code [path/to/folder]
```

Put the .bat file on Desktop, and double click it to run. [] means optional.

If you see "Hello, world!" in the screen, then you successfully set up a C++ environment.

It will create .vscode folder automatically.

# 2. CMake

Read this article, it says Linux, but it can be used on Windows as well:

[Get started with CMake Tools on Linux](https://code.visualstudio.com/docs/cpp/cmake-linux)

# 3. OpenGL

See README.md in MinGW folder of this project.(Section 2.1~2.3) 

Note to copy glfw3.lib in lib-vc2022

# 4. The End

Now you have everything done. 

Then open the root folder in VSCode and use CMake to build and run program. If the run button of CMake in VSCode doesn't work, you can find the exe file in OpenGL/build/Debug. If you get a Hexagonal Star, then you successfully set up an OpenGL environment:

![](https://pic2.zhimg.com/80/v2-154375a9d0d2e84b3e4c4867c58f8351_720w.webp)

# 5. Reference

[写个脚本来解决使用VScode调试C程序时，提示“仅当从 VS 开发人员命令提示符处运行 VS Code 时，cl.exe 生成和调试才可用。”的问题](https://www.cnblogs.com/CoronaZero/p/16656816.html)
