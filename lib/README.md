+ pkgconfig下是编译 Cairo-1.16.0 时需要的链接信息，其中的依赖位于 dep，均来自 emacs，在要编译Cairo-1.16.0时，在git bash下使用mingw编译的话，需要设置git bash的环境变量，以时其`./configure`工具调用`pkg-config.exe`时能够找到各个库的位置；

  在git安装根目录下：`ProtableGit/etc/bash.bashrc`文件的最后，添加环境变量：

  ```
  export PKG_CONFIG_PATH=/d/OpenFree/Cairo-1.16.0/lib/pkgconfig
  export LD_LIBRARY_PATH=/d/OpenFree/Cairo-1.16.0/lib/dep
  ```

  然后使用：`pkg-config.exe --libs pixman-1`检查是否输出正确；

  若执行./configure后找不到提示pkg-config找不到libpng，则可以在git bash中输入：`export png_REQUIRES="install_dir/libpng.a" `以添加一个环境变量；

  最后，在git bash中输入：

  ```
  ./configure --enable-gl=yes --enable-wgl=yes
  ```

  其中`--enbale-gl=yes`使能OpenGL，而`--enable-wgl=yes`特定于windows平台的OpenGL，若在linux下，则是`--enable-glx=yes`

  这样，就生成了可用的makefile文件，然后就可以开始编译了。


+ **libcairo-2.dll.a** 是为了避免与 **libcairo.a** 在链接时冲突而改名了的，原本名称为 **libcairo.dll.a**

- 支持Cairo的程序的最小依赖库（只需要链接./dep文件下的）：

  ```
  libbz2.a
  libexpat.a
  libfontconfig.a
  libfreetype.a
  libgraphite2.a
  libharfbuzz.a
  libintl.a
  libpixman-1.a
  libpng-9.a
  libz-9.a
  
  rpcrt4
  ```

  `rpcrt4`是再windows平台中必须使用的，rpcrt4是windows系统的dll

  在运行编译后的程序时，还需要`libglib.dll`, `libiconv.dll`, `libpcre.dll` 这3个库

  

- `libcairo-gl.a`是编译Cairo-1.16.0时，使能了`--enable-gl=yes`，`--enable-wgl=yes`选项的库，作用是支持OpenGL

- `libcairo-gl-strip.a`是strip掉调试符号的`libcairo-gl.a`版本

