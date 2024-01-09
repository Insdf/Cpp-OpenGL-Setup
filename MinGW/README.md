[中文](README_CN.md)

Assuming that using Windows platform, VSCode and installing MinGW by MSYS2.

On Windows, many projects only have pre-built binaries for MSVC, so maybe it is a better choice. If you still want to use MinGW, you can find that if the library you need can be installed using MSYS2 or vcpkg.

# 1. C++

Read this article:

[C/C++ for Visual Studio Code](https://code.visualstudio.com/docs/languages/cpp)

After setup, you can open the root folder of this project in VSCode, and run `hello_world/hello_world.cpp`, and choose g++.exe. If you see "Hello, world!" in the screen, then you successfully set up a C++ environment.

It will create .vscode folder automatically.

# 2. OpenGL

## 2.1. Download

In Windows, if you can find `opengl32.dll` in C:/Windows/System32, then you have OpenGL installed. Other platforms are similar. If not, read this:

[Downloading OpenGL](https://www.khronos.org/opengl/wiki/Getting_Started#Downloading_OpenGL)

Except OpenGL, you need another two libraries to help you use OpenGL, one is a window toolkit, the other is an OpenGL loading library. In this article, we choose GLFW and GLAD. This project already includes them, but you can download them by yourself.

## 2.2. GLFW

Go to the official website [GLFW](https://www.glfw.org/download.html) to download it. If you are a experienced developer, you can download source package and build it from source using CMake. 

If you are a beginner, you can download pre-compiled binaries, which have two versions for Windows and MacOS. If you are using Linux, you can get GLFW from your package system, for example, apt on Ubuntu.

After downloading the zip file, extract it. 

Again you can open the root folder of this project (Abbreviated as: OpenGL/), which has two subfolders in it. One is "include", for .h header files, and the other is "lib", for libraries, say .lib/.dll/.a/.c etc. 

Move contents in glfw-x.x.x.bin.WIN64 (or MACOS)/include/ to OpenGL/include/, and glfw-x.x.x.bin.WIN64/lib-mingw-w64/libglfw3.a to OpenGL/lib/. On MacOS, you may copy contents according to your hardware architecture (e.g. lib-x86_64).

## 2.3. GLAD

Read the last section "Setting up GLAD" in this:

[Learn OpenGL](https://learnopengl.com/Getting-started/Creating-a-window)

Move glad/include/ to OpenGL/include/, glad/src/glad.c to OpenGL/lib/

## 2.4. VSCode

It's a better choice to use CMake, because it can cross compiler and platform:

[Get started with CMake Tools on Linux](https://code.visualstudio.com/docs/cpp/cmake-linux)

It says Linux, but it can be used on Windows as well.

You can also configure VSCode like below.

There are four files in `MinGW/.vscode` folder : c_cpp_properties.json, launch.json, tasks.json and settings.json. You can use them directly if you choose default folder (C:/msys64) when installing MSYS2. But I need to make some clarifications here.

You need to configure the 2 folders: include and lib.

1\) include

All files are .h files. You should first add 

"${workspaceFolder}/include/**" 

in "includePath" of c_cpp_properties.json file. "\*\*" means search in the folder recursively.

Then you should add 

"-I", 

"${workspaceFolder}\\\\include"

in "args" of tasks.json to make it work.

2\) lib

First you should add 

"${workspaceFolder}/lib/**"

in "includePath" of c_cpp_properties.json file.

The following configurations concerning lib are all in "args" of tasks.json.

For .a/.c files, put them after "-g", e.g.:

"-g",

"${workspaceFolder}\\\\lib\\\\**.a",

"${workspaceFolder}\\\lib\\\\**.c",

\*\*.a means all files with extension .a in the folder. Note to add "," if there are other lines after your input.

If you use .dll files, you first need to tell VSCode where to find them, use "-L":

"-L",

"${workspaceFolder}\\\\lib",

then use "-l" to link to .dll file, note that for every .dll file you need a "-l" before it, you can omit the .dll extension:

"-l",

"glfw3",

Now you have configured GLFW and GLAD with VSCode, but there are some other .dll files you need to let your program runn normally.

They are .dll files in C:/Windows/System32, so you need not to specify the folder using "-L", just add them:

"-l",

"opengl32", 

"-l",

"gdi32",

Similarly, there are still "kernel32.dll", "user32.dll" etc. Add them if you need.

Note that these are all .dll files, and you should figure out  by yourself that how to configure .lib or .dylib file.

By the way, if you install MYSY2 in other directory, you should modify the path to g++.exe/gcc.exe/gdb.exe in those json files manually.

# 3. The End

Now you have everything done.

Then open the root folder in VSCode and use CMake to compile and run program. If the run button of CMake in VSCode doesn't work, you can find the exe file in OpenGL/build. You can also move MinGW/.vscode to root folder and run `hello_hexagonal_star.cpp`. If you get a Hexagonal Star, then you successfully set up an OpenGL environment:

![](https://pic2.zhimg.com/80/v2-154375a9d0d2e84b3e4c4867c58f8351_720w.webp)
