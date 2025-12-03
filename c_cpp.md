## 配置C/C++ 编译器

### windows

- 下载[MinGW](https://github.com/niXman/mingw-builds-binaries/releases)并根据自己电脑的版本选择合适的压缩包 ![version](assets/version.png)
- 解压安装包并安装，记录安装路径
- 配置环境变量
    - 右键`此电脑` -> `属性` -> `高级系统设置` -> `环境变量`
    - 在系统变量中找到`PATH`，点击`编辑`
    - 新建添加MinGW-w64的bin目录路径，例如`D:\Program\mingw64\bin`
- 打开终端输入
    ```bash 
    gcc --version
    g++ --version
    gdb --version
    ```
    若出现了版本提示，则安装成功

### Linux

- 打开终端，输入 
    ```bash 
    gcc --version
    g++ --version
    gdb --version
    ```
    若出现了版本提示，可跳过安装编译器部分
- 未出现版本信息，则运行
    ```bash
    sudo apt install g++
    sudo apt install gcc
    sudo apt install gdb
    ```
- 出现安装请求提示时，键入 y 并按回车，完成安装

### Mac

- 打开终端，输入 
    ```bash 
    clang --version
    ```
    若出现了版本提示，输入
    ```bash
    g++ --version
    gdb --version
    ```
    若出现版本提示则已经可以运行

- clang未安装，则运行
    ```bash
    xcode-select --install
    ```
    安装完成后，再次验证clang版本

## VSCode C/C++ 插件

### 安装插件

- 打开扩展-应用商店 ![应用商店](assets/CExtension.png)
- 搜索C++，安装图示插件 ![C/C++扩展](assets/CExtension2.png)

### 配置插件

#### 1. Compiler Path (编译器路径)
IntelliSense 需要知道你用什么编译器，以便它能自动找到标准库头文件（如 `<iostream>`, `<stdio.h>`）。
* 点击右侧齿轮按钮，选择设置![设置](assets/Settings.png)
* 搜索 compiler， 找到Compiler Path, 选择 在设置中编辑![Path](assets/compiler.png)
* 在终端中输入
    ```bash
    # Windows
    where.exe g++
    ```

    ```bash
    # Mac/Linux
    whereis g++
    ```
* 将找到的g++路径写入settings.json的 **"C_Cpp.default.compilerPath": ""** (windows需要在每个反斜杠处多加一个反斜杠
    *   **Windows (MinGW)**: 例如 `C:/MinGW/bin/gcc.exe` 或 `C:/MinGW/bin/g++.exe`。
    *   **Linux/macOS**: 例如 `/usr/bin/gcc` 或 `/usr/bin/clang`。

#### 2. IntelliSense Mode (智能感知模式)
这个选项告诉 VS Code 模拟哪种架构，以便正确解析指针大小等。
*   **Windows**: 通常选 `windows-gcc-x64` (MinGW) 或 `windows-msvc-x64` (Visual Studio)。
*   **Linux**: 通常选 `linux-gcc-x64`。
*   **macOS**: 通常选 `macos-clang-arm64`。
*   *如果不确定，通常选 `gcc-x64` (通用) 也能工作。*

#### 3. Include Path (包含路径)
如果你的代码引用了**非标准库**的头文件（例如你自己写的头文件在 `include/` 目录下，或者使用了第三方库如 OpenCV），你需要在这里添加路径，否则会报错 `#include errors detected`。
*   默认会有 `${workspaceFolder}/**`，表示递归搜索当前工作区的所有文件夹。
*   如果是第三方库，点击“添加项”，输入绝对路径，例如：
    *   `C:/opencv/build/include`
    *   `/usr/local/include/eigen3`

#### 4. C/C++ Standard (语言标准)
选择你项目中使用的标准版本（如 `c++17`, `c++20`, `c11` 等），以确保 IntelliSense 不会误报语法错误。

### 验证配置 (c_cpp_properties.json)
示例：
```json
{
    "C_Cpp.default.compilerPath": "C:\\mingw64\\bin\\g++.exe",
    "C_Cpp.default.cppStandard": "c++17",
    "C_Cpp.default.cStandard": "c11",
    "C_Cpp.default.intelliSenseMode": "windows-gcc-x64"
}
```
