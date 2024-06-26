# Build Getgud C++ SDK

Getgud C++ SDK allows you to integrate your game with the GetGud platform. Once integrated, you will be able to stream your matches to Getgud's cloud, as well as to send reports and update player's data. This README will include all possible build instructions for different systems.


<b>[IMPORTANT]</b> Before you start clone Getgud SDK repo **recursively**
```
git clone https://github.com/getgud-io/cpp-getgud-sdk-dev --recursive
cd cpp-getgud-sdk-dev
```

## Table of Contents

- [Build for Linux](https://github.com/getgud-io/getgud-docs/blob/main/1-Integrations/cpp-build-instructions.md#build-for-linux)
- [Build for Windows](https://github.com/getgud-io/getgud-docs/blob/main/1-Integrations/cpp-build-instructions.md#build-for-windows)
- [Build for Unreal Engine](https://github.com/getgud-io/getgud-docs/blob/main/1-Integrations/cpp-build-instructions.md#build-for-unreal-engine)
- [Build for Unity](https://github.com/getgud-io/getgud-docs/blob/main/1-Integrations/cpp-build-instructions.md#build-for-unity)

## Build for Linux

### Requirements:
- CMake
- make
- gcc and g++
- libcurl development tools
- libssl
- libcrypto
- openssl development tools

Before building install all required libraries
```
sudo apt update
sudo apt-get install git binutils make csh g++ sed gawk autoconf automake autotools-dev shtool libtool curl cmake libssl-dev libpsl-dev
```

To start the build process run our predefined script
```
cd ./cpp-getgud-sdk-dev/tools
sh linuxbuild_so.sh
```

Congrats, SDK is built! You will mostly need `getgudsdk.a` and `getguddsk.so` files for Linux.
 
## Build for Windows

### Requirements:
- [CMake](https://cmake.org/download/)
- [make, available through Visual Studio](https://visualstudio.microsoft.com/downloads/)
- x64 Native Tools Command Prompt, available through Visual Studio

<b>[IMPORTANT]</b> All commands should run in **x64 Native Tools Command Prompt**

First we need to build libcurl and zlib which are used inside SDK

### libcurl

Go to libcurl directory

```bash
cd cpp-getgud-sdk-dev\libs\libcurl
```

Build libcurl
```bash
set RTLIBCFG=static
call .\buildconf.bat
cd .\winbuild
call nmake /f Makefile.vc mode=static vc=17 debug=yes
call nmake /f Makefile.vc mode=static vc=17 debug=no
```

### zlib

Go to zlib directory

```bash
cd cpp-getgud-sdk-dev\libs\zlib
```

Build zlib
```bash
call nmake /f win32/Makefile.msc
```

Now that we have build libraries that we need, let's build SDK itself.
Go to SDK root folder:
```bash
cd cpp-getgud-sdk-dev
```

Build SDK:

```bash
cmake -DDLL_BUILD:STRING=True .
cmake --build .
cmake --build . --config Release
```

Congrats, SDK is built! Your build files should be located in `_build` folder.

## Build for Unreal Engine

To build and integrate for UE follow [this tutorial](https://github.com/getgud-io/getgud-docs/blob/main/1-Integrations/Unreal%20Engine/unreal-engine-integration.md)


## Build for Unity

1. To build and integrate for Unity you should build SDK for your Windows/Linux server as described in our tutorials.
2. Integrate SDK build files into Unity as described in [this tutorial](https://github.com/getgud-io/getgud-docs/blob/main/1-Integrations/Unity/unity-integration.md)


