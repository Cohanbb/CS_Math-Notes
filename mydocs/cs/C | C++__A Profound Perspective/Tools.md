# 开发工具

## GCC

GCC(GNU Compiler Collection) 是 C\C++ 最主流的编译器之一，是完全开源、自由的软件。运行平台主要是 UNIX/Linux 系统，在 Windows 上也可以通过 MinGW 使用 GCC。

GCC 原名为 GNU C Compiler，即 GNU C 语言编译器。但目前支持多种语言， 包括 C、C++、Objective-C、Fortran、Java 和 Go 语言。

**GCC 的使用方法**

## GDB

GDB(GNU Symbolic Debugger) 是完全开源、自由的程序调试工具。

**GDB 的使用方法**

## Make

对于单个 C\C++ 程序，直接使用 GCC 进行编译即可生成可执行文件。而对于含有多个 C\C++ 程序的项目，如果每个程序都用 GCC 编译则过于复杂。使用 Make 工具可以简明地表示文件之间的包含关系，自动完成编译。

make 工具根据编写的 makefile 处理项目的构建和编译。

**makefile 的编写方法**

## CMake

当项目十分庞大时 makefile 也会非常的难写，于是产生了 cmake，根据编写的 cmakelist 自动生成 makefile。

cmakelist

