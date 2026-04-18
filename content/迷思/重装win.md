重装win的时候踩了很多大坑，而且不知道为什么。除了不能直接重装win11以外，主要还是聚焦于环境之上

下面两个应该都要装:

## msys2

提供类unix环境, 尽量使用mingw以保证兼容，可以在mingw的terminal里使用 `pacman -S mingw-w64-x86_64-toolchain` 来安装所有依赖

## mcvs

构建原生windows要用的c/c++ compiler

## winget

超级大坑，几乎能想到的东西都可以用这个装，win10没有。但是这个只能从microsoft store上下载，但是自己还搜不到，官网也没有更新下载地址，后来在其他doc上找到了
[App Installer](https://apps.microsoft.com/detail/9nblggh4nns1?hl=en-US&gl=CA)
