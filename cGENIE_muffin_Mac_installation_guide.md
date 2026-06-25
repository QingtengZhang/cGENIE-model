# cGENIE.muffin Mac 安装手册

本文档记录如何在 macOS 上安装、配置并验证 `cGENIE.muffin` Earth system model。内容基于官方仓库与一次在 Apple silicon Mac 上的实际部署过程整理，上传到 GitHub 作为可复现安装说明。

## 适用环境

本文档适用于：

- macOS
- Apple silicon Mac，例如 M1、M2、M3、M4
- Intel Mac
- Homebrew 管理依赖
- `cGENIE.muffin` 的 `master.python3` 分支

实际验证环境：

- macOS，Apple silicon，`arm64`
- Homebrew 路径：`/opt/homebrew`
- GNU Fortran：Homebrew GCC 15.2.0
- netCDF：Homebrew netcdf 4.9.3
- netCDF Fortran：Homebrew netcdf-fortran 4.6.2
- 测试命令：`make testbiogem`
- 测试结果：`**TEST OK**`

## 官方资源

- cGENIE.muffin 主仓库：<https://github.com/derpycode/cgenie.muffin>
- muffindoc 文档仓库：<https://github.com/derpycode/muffindoc>
- Mac 安装 PDF：<https://github.com/derpycode/muffindoc/blob/master/muffin3.install.MacOS.pdf>

## 目录规划

官方配置默认把源码放在用户家目录下：

```bash
~/cgenie.muffin
```

默认输出目录为：

```bash
~/cgenie_output
```

建议使用上述默认目录。原因是 cGENIE 的 Makefile 和运行脚本比较老，路径中如果包含空格，可能导致编译或运行阶段路径被错误拆分。例如不建议把源码最终安装在：

```bash
~/Documents/New project/cgenie.muffin
```

这样的路径中，因为 `New project` 中间有空格。

## 第 1 步：安装 Xcode Command Line Tools

先安装 Apple 的命令行开发工具：

```bash
xcode-select --install
```

如果系统提示已经安装，可以跳过。

检查：

```bash
xcode-select -p
```

正常情况下会输出类似：

```text
/Applications/Xcode.app/Contents/Developer
```

或：

```text
/Library/Developer/CommandLineTools
```

## 第 2 步：安装 Homebrew

如果还没有安装 Homebrew，执行：

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

安装后检查：

```bash
brew --version
brew doctor
```

Apple silicon Mac 上 Homebrew 通常位于：

```bash
/opt/homebrew
```

Intel Mac 上 Homebrew 通常位于：

```bash
/usr/local
```

## 第 3 步：安装编译和 netCDF 依赖

执行：

```bash
brew install cmake
brew install gcc
brew install hdf5
brew install netcdf
brew install netcdf-fortran
brew install netcdf-cxx
brew install wget
```

检查 Fortran 编译器：

```bash
which gfortran
gfortran --version
```

Apple silicon Mac 上通常应看到：

```text
/opt/homebrew/bin/gfortran
```

检查 netCDF：

```bash
which nc-config
which nf-config
nc-config --prefix
nf-config --prefix
```

还可以检查 netCDF Fortran 模块文件是否存在：

Apple silicon：

```bash
ls /opt/homebrew/include/netcdf.mod
ls /opt/homebrew/lib/libnetcdf.dylib
ls /opt/homebrew/lib/libnetcdff.dylib
```

Intel Mac：

```bash
ls /usr/local/include/netcdf.mod
ls /usr/local/lib/libnetcdf.dylib
ls /usr/local/lib/libnetcdff.dylib
```

## 第 4 步：克隆 cGENIE.muffin

建议直接克隆官方推荐的 Python 3 分支：

```bash
cd ~
git clone --branch master.python3 https://github.com/derpycode/cgenie.muffin.git cgenie.muffin
```

如果网络较慢，也可以使用浅克隆：

```bash
cd ~
git clone --depth 1 --branch master.python3 https://github.com/derpycode/cgenie.muffin.git cgenie.muffin
```

进入源码目录：

```bash
cd ~/cgenie.muffin
git branch --show-current
```

应输出：

```text
master.python3
```

## 第 5 步：配置 `user.mak`

进入主构建目录：

```bash
cd ~/cgenie.muffin/genie-main
```

编辑：

```bash
nano user.mak
```

也可以用 VS Code、Vim 或其他编辑器。

### 5.1 配置机器类型

找到：

```makefile
MACHINE=LINUX
#MACHINE=OSX	# Intel processor
#MACHINE=OSX_M	# Apple silicon (M1, M2 etc.)
```

Apple silicon Mac 修改为：

```makefile
#MACHINE=LINUX
#MACHINE=OSX	# Intel processor
MACHINE=OSX_M
```

Intel Mac 修改为：

```makefile
#MACHINE=LINUX
MACHINE=OSX
#MACHINE=OSX_M	# Apple silicon (M1, M2 etc.)
```

注意：Apple silicon 上建议把 `MACHINE=OSX_M` 写成单独一行，不要在同一行后面保留注释。推荐：

```makefile
MACHINE=OSX_M
```

不推荐：

```makefile
MACHINE=OSX_M	# Apple silicon (M1, M2 etc.)
```

某些旧版 `make` 解析时可能把行内注释一起当作变量值，导致 Apple silicon 判断失效，进而错误加入 Intel 专用编译参数 `-msse`。

### 5.2 配置 netCDF 路径

找到：

```makefile
NETCDF_DIR=/usr/local
```

Apple silicon Mac 修改为：

```makefile
NETCDF_DIR=/opt/homebrew
```

Intel Mac 通常保持：

```makefile
NETCDF_DIR=/usr/local
```

如果不确定 Homebrew 路径，可以执行：

```bash
brew --prefix
```

然后把输出路径写入 `NETCDF_DIR`。

### 5.3 确认编译器设置

`user.mak` 中通常默认已有：

```makefile
F77=gfortran
CC=gcc
CXX=g++
```

一般不需要修改。

macOS 上 `/usr/bin/gcc` 实际通常是 Apple clang。cGENIE 主要依赖 `gfortran`，所以只要 `gfortran` 来自 Homebrew 并可用即可。

## 第 6 步：检查关键配置

在 `~/cgenie.muffin/genie-main` 中执行：

```bash
grep -n "MACHINE=" user.mak
grep -n "NETCDF_DIR=" user.mak
```

Apple silicon 上应看到类似：

```text
#MACHINE=LINUX
MACHINE=OSX_M
NETCDF_DIR=/opt/homebrew
```

可以进一步检查 `make` 展开的编译参数中是否没有 `-msse`：

```bash
make -pn testbiogem | grep "^FFLAGS"
```

Apple silicon 上不应出现：

```text
-msse
```

如果出现，说明 `MACHINE=OSX_M` 没有被正确识别。

## 第 7 步：编译并运行官方测试

在 `~/cgenie.muffin/genie-main` 中执行：

```bash
make testbiogem
```

第一次运行会编译大量 Fortran 文件，输出很多 warning 是正常的，例如：

- rank mismatch warning
- conversion warning
- unused dummy argument warning
- duplicate Makefile target warning

只要没有 `Error` 并最终通过测试即可。

成功时末尾会看到类似：

```text
Files /Users/yourname/cgenie_output/genie_eb_go_gs_ac_bg_regtest/biogem/fields_biogem_3d.nc and /Users/yourname/cgenie.muffin/genie-knowngood/genie_eb_go_gs_ac_bg_knowngood/biogem/fields_biogem_3d.nc match
**TEST OK**
```

这表示：

- `genie.exe` 编译成功
- `nccompare.exe` 编译成功
- 测试实验运行完成
- 输出文件与官方 knowngood 文件匹配

## 第 8 步：输出目录

测试运行后，默认输出在：

```bash
~/cgenie_output
```

例如：

```bash
~/cgenie_output/genie_eb_go_gs_ac_bg_regtest
```

测试日志位于：

```bash
~/cgenie.muffin/genie-main/testbiogem.out
```

当前配置记录位于：

```bash
~/cgenie.muffin/genie-main/current_config.dat
```

## 常用命令

进入主目录：

```bash
cd ~/cgenie.muffin/genie-main
```

重新运行测试：

```bash
make testbiogem
```

清理全部编译产物：

```bash
make cleanall
```

清理后重新测试：

```bash
make cleanall
make testbiogem
```

查看测试结果：

```bash
grep -B1 "**TEST" testbiogem.out
```

## 常见问题

### 1. Apple silicon 报错：`gfortran: error: unrecognized command-line option '-msse'`

原因：

`-msse` 是 Intel CPU 专用编译参数。Apple silicon 是 ARM 架构，不支持该参数。

解决：

检查 `~/cgenie.muffin/genie-main/user.mak`：

```makefile
MACHINE=OSX_M
```

确保这一行没有行内注释。推荐写成：

```makefile
MACHINE=OSX_M
```

然后清理并重试：

```bash
cd ~/cgenie.muffin/genie-main
make cleanall
make testbiogem
```

### 2. 找不到 `netcdf.mod`

报错可能类似：

```text
Cannot open module file 'netcdf.mod'
```

先检查文件：

Apple silicon：

```bash
ls /opt/homebrew/include/netcdf.mod
```

Intel Mac：

```bash
ls /usr/local/include/netcdf.mod
```

如果不存在，重新安装：

```bash
brew install netcdf-fortran
```

然后检查 `user.mak` 中的 `NETCDF_DIR`。

Apple silicon：

```makefile
NETCDF_DIR=/opt/homebrew
```

Intel Mac：

```makefile
NETCDF_DIR=/usr/local
```

### 3. 链接阶段找不到 `-lnetcdf` 或 `-lnetcdff`

检查动态库：

Apple silicon：

```bash
ls /opt/homebrew/lib/libnetcdf.dylib
ls /opt/homebrew/lib/libnetcdff.dylib
```

Intel Mac：

```bash
ls /usr/local/lib/libnetcdf.dylib
ls /usr/local/lib/libnetcdff.dylib
```

如果不存在：

```bash
brew reinstall netcdf
brew reinstall netcdf-fortran
```

### 4. 路径里有空格导致编译或运行异常

不建议把源码安装到带空格的路径，例如：

```bash
~/Documents/New project/cgenie.muffin
```

建议安装到：

```bash
~/cgenie.muffin
```

如果已经克隆到带空格的目录，可以复制到家目录：

```bash
ditto "/path/with spaces/cgenie.muffin" ~/cgenie.muffin
```

然后在新目录中重新测试：

```bash
cd ~/cgenie.muffin/genie-main
make cleanall
make testbiogem
```

### 5. `make testbiogem` 输出大量 warning

这是正常现象。cGENIE 包含大量历史 Fortran 代码，现代 `gfortran` 会输出较多 warning。

只要最终出现：

```text
**TEST OK**
```

就表示安装验证通过。

### 6. GitHub 克隆很慢或中断

可以使用浅克隆：

```bash
git clone --depth 1 --branch master.python3 https://github.com/derpycode/cgenie.muffin.git cgenie.muffin
```

如果普通克隆失败，不一定是配置问题，可能只是网络连接不稳定。

## 最小可复现安装流程

下面是 Apple silicon Mac 上的最小命令汇总：

```bash
xcode-select --install

brew install cmake gcc hdf5 netcdf netcdf-fortran netcdf-cxx wget

cd ~
git clone --depth 1 --branch master.python3 https://github.com/derpycode/cgenie.muffin.git cgenie.muffin

cd ~/cgenie.muffin/genie-main
```

编辑 `user.mak`：

```makefile
#MACHINE=LINUX
MACHINE=OSX_M
NETCDF_DIR=/opt/homebrew
```

然后执行：

```bash
make cleanall
make testbiogem
```

成功标志：

```text
**TEST OK**
```

## 参考配置示例

Apple silicon Mac 的 `user.mak` 关键配置：

```makefile
GENIE_ROOT        = $(HOME)/cgenie.muffin
OUT_DIR           = $(HOME)/cgenie_output
RUNTIME_ROOT      = ../../cgenie.muffin

F77=gfortran
CC=gcc
CXX=g++

BUILD=SHIP

#MACHINE=LINUX
#MACHINE=OSX
MACHINE=OSX_M

MODEXT=mod

NETCDF_DIR=/opt/homebrew
NETCDF_NAME=netcdf
NETCDF_LINK_FLAGS=-L$(NETCDF_DIR)/lib -lnetcdf -lnetcdff
```

Intel Mac 的 `user.mak` 关键配置：

```makefile
GENIE_ROOT        = $(HOME)/cgenie.muffin
OUT_DIR           = $(HOME)/cgenie_output
RUNTIME_ROOT      = ../../cgenie.muffin

F77=gfortran
CC=gcc
CXX=g++

BUILD=SHIP

#MACHINE=LINUX
MACHINE=OSX
#MACHINE=OSX_M

MODEXT=mod

NETCDF_DIR=/usr/local
NETCDF_NAME=netcdf
NETCDF_LINK_FLAGS=-L$(NETCDF_DIR)/lib -lnetcdf -lnetcdff
```

## 卸载或清理

删除源码：

```bash
rm -rf ~/cgenie.muffin
```

删除模型输出：

```bash
rm -rf ~/cgenie_output
```

删除 Homebrew 依赖时请谨慎，因为这些依赖可能被其他软件使用。

## 备注

如果曾经在其他目录中临时克隆过一份 `cgenie.muffin`，例如：

```bash
~/Documents/New project/cgenie.muffin
```

并且已经确认正式安装目录：

```bash
~/cgenie.muffin
```

可以正常通过：

```bash
cd ~/cgenie.muffin/genie-main
make testbiogem
```

那么临时克隆目录可以删除，不影响正式安装。
