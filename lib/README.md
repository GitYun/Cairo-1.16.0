+ pkgconfig下是编译 Cairo-1.16.0 时需要的链接信息，其中的依赖位于 dep，均来自 emacs，在要编译Cairo-1.16.0时，将 dep 目录下的内容拷贝到 lib 目录下（因为 pkgconfig 下文件链接信息是基于lib目录的，也可以改pkgconfig文件，不过有点儿多）
+ **libcairo-2.dll.a** 是为了避免与 **libcairo.a** 在链接时冲突而改名了的，原本名称为 **libcairo.dll.a**

