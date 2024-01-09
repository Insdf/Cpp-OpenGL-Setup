假设使用Windows平台，VSCode并通过VS Build Tool安装MSVC。

在Windows上，可以看看你需要的项目是否可以通过MSYS2或vcpkg安装。

这次不想再配置VSCode，所以我们使用CMake，一个跨编译器和平台的编译工具。

# 1. C++

可以看这篇文章:

[C/C++ for Visual Studio Code](https://code.visualstudio.com/docs/languages/cpp)

设置完成后，你可以在VSCode中打开此项目中的根文件夹，运行`hello_world.cpp`，然后选择cl.exe.

注意你应该先通过Developer Command Prompt打开VSCode，一个.bat文件可能会有帮助：

```batch
@echo off

call "C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools\Common7\Tools\VsDevCmd.bat"

code [path/to/folder]
```

将.bat文件放在桌面，双击打开就可以了，[]意思是可选项。

如果你在屏幕中看到"Hello, world!"，则表示你已成功设置C++环境。

它会自动创建.vscode文件夹。

# 2. CMake

阅读这篇文章，它说是Linux，但Windows上也适用：

[Get started with CMake Tools on Linux](https://code.visualstudio.com/docs/cpp/cmake-linux)

# 3. OpenGL

阅读此项目MinGW文件夹中的README_CN.md (2.1~2.3小节) 

注意复制 lib-vc2022 中的glfw3.lib

# 4. 结语

现在你已经完成了一切。

然后在VSCode中打开根文件夹，使用CMake编译运行程序，如果VSCode中的CMake运行按钮不起作用，你可以在OpenGL/build/Debug中找到exe程序。如果你得到一个六茫星，那么你已成功搭建OpenGL环境：

![](https://pic2.zhimg.com/80/v2-154375a9d0d2e84b3e4c4867c58f8351_720w.webp)

# 参考

[写个脚本来解决使用VScode调试C程序时，提示“仅当从 VS 开发人员命令提示符处运行 VS Code 时，cl.exe 生成和调试才可用。”的问题](https://www.cnblogs.com/CoronaZero/p/16656816.html)
