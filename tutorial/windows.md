[<-- Home](/)

# TEK 5030 - Getting started with C++ on Windows

In this guide we will explain how to use Visual Studio, Conan and CMake to make the C++ coding experience in windows a comfortable experience.
- Visual Studio will be our IDE, where we edit/debug, compile and run our code.
- CMake is a program that will build our projects properly, and on windows with Visual Studio, it will create a Visual Studio project for us.
- Conan is a so called C++ packet manager that will help us in managing any third party C++ libraries that we want to use in our projects.

In addition to these programs, you will need a terminal for entering commands.
This can be windows' cmd.exe (Quick access: Press WIN + r, type in "cmd" and press enter) or something similar.
Git for windows (freely available for download at https://gitforwindows.org/) comes with Git BASH which is a nice alternative that also allows you to interact with git repositories.

Let us start by installing what we need and create a first C++ project:

## Downlad and install Visual Studio 2022
Visual Studio Community edition is freely available for download at https://visualstudio.microsoft.com/downloads/.
Download and install it somewhere convenient on your computer.
During the installation process you will be asked to choose exactly which components of Visual Studio you want to install.
Make sure to install "Desktop development with C++".
Default settings will probably be ok.

## Downlad and install CMake
CMake is freely availble for download at https://cmake.org/download/.
We suggest the latest Windows x64 Installer (currently this is: cmake-3.25.2-windows-x84_64.msi)
Download and install it somewhere convenient on your computer.

## Downlad and install Conan
Conan is freely available for download at https://conan.io/downloads.html.
If you already have python installed, you can run ```pip install conan```.
Otherwise, you can install Conan using the windows installer labeled x86_64.

## Choosing a Conan data folder
Conan will be responsible for downloading any thirdparty dependencies, e.g. OpenCV, that we want to use in our projects.
You can chose where you want Conan to store its data, by creating the windows environment variable CONAN_USER_HOME.
On the environment variable panel, choose to create a ```New...``` user variable.
Let the ```Variable name``` be ```CONAN_USER_HOME``` and let the ```Variable value``` be the path to a convenient folder on your computer, e.g. ```C:\tek5030\ConanData```.
Click ```OK``` to create the user variable and ```OK``` once more to exit the environment variable panel.

## Creating a first program with a third party dependency
Start by creating an empty folder ```test``` where you want to store your C++ projects.
In this folder, create three text files: ```conanfile.txt```, ```CMakeLists.txt``` and ```main.cpp```.

conanfile.txt describes what third party C++ libraries we want to use in our project.
In this basic example, we only want to test out the linear algebra library Eigen version 3.4.0.
Then the file should look like this:
```
[requires]
eigen/3.4.0

[generators]
cmake_find_package
virtualrunenv

```

CMakeLists.txt describes how we want CMake to build our project.
For our basic test program, it should look like this:
```
cmake_minimum_required( VERSION 3.5.1 )

project(test)
list(PREPEND CMAKE_MODULE_PATH ${CMAKE_BINARY_DIR})

# Find libraries
find_package(Eigen3 REQUIRED)

set(exe_name test)

add_executable(${exe_name}
  main.cpp
  )

target_link_libraries(${exe_name}
  Eigen3::Eigen
  )

set_target_properties(${exe_name} PROPERTIES
  CXX_STANDARD_REQUIRED ON
  CXX_STANDARD 17
  )

set(gcc_like_cxx "$<COMPILE_LANG_AND_ID:CXX,ARMClang,AppleClang,Clang,GNU,LCC>")
set(msvc_cxx "$<COMPILE_LANG_AND_ID:CXX,MSVC>")

target_compile_options(${exe_name} PRIVATE
  "$<${gcc_like_cxx}:$<BUILD_INTERFACE:-Wall;-Wextra;-Wpedantic;-Wshadow;-Wformat=2>>"
  "$<${msvc_cxx}:$<BUILD_INTERFACE:-W4;-MD>>"
)

target_compile_definitions(${exe_name} PUBLIC
  "$<${msvc_cxx}:-D_USE_MATH_DEFINES>"
)

```
Our only C++ project file is ```main.cpp```.
It will only create and print a 3x3 matrix.
main.cpp can then look like this:
```
#include "Eigen/Eigen"
#include <iostream>

int main()
{
  // Create and display a matrix A.
  Eigen::Matrix3d A;
  A << 1.0, 2.0, 3.0,
       4.0, 5.0, 6.0,
       7.0, 8.0, 9.0;

  std::cout << "A = " << std::endl << A << std::endl;
}

```

In order to download Eigen 3.4.0 and build a Visual Studio project for us, we need to enter the following commands from within the project folder:

```bash
conan install . -if build -b missing
cd build
cmake ..
cmake --build .
```

Afterwards, if all went well, we should find ```test.sln``` within the ```build``` folder.
Doubleclicking ```test.sln``` should open the project in Visual Studio.
The first time we open the project, you will notice three projects in the ```Solution Explorer``` window in Visual Studio: ```ALL_BUILD```, ```test``` and ```ZERO_CHECK```.
Right click on ```test``` and select ```Set as startup project```.
Now you should be able to run the program by pressing the green triangle in Visual Studio (shortcut F5).

If you were able to get through this tutorial and ended up with a working C++ project, you should be able to download (git clone) and play around with this years tek5030 labs.

Good luck with the rest of tek5030!
