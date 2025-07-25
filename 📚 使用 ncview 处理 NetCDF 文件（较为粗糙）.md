`ncview` 是一个用于 **可视化 NetCDF（Network Common Data Form）数据文件** 的轻量级图形界面工具，主要用于快速查看和浏览 `.nc` 格式的数据文件（常用于气象、海洋、遥感等科学领域）。

---

### 🔍 ncview 简介
+ **作者**：David W. Pierce 博士
+ **用途**：快速浏览 NetCDF 数据、动画播放时间序列、查看变量、剖面显示、切片等。
+ **界面**：运行于基于 X11 的窗口环境下，图形界面简洁直观。
+ **适用平台**：主要用于类 UNIX 系统（如 Linux 和 macOS），Windows 下不原生支持但可通过 WSL 使用
+ **参考链接**：[https://cirrus.ucsd.edu/ncview/](https://cirrus.ucsd.edu/ncview/)

---

### ⚙️ ncview 安装方法
#### ✅ macOS 系统
推荐使用 [Homebrew](https://brew.sh/) 来安装：

```shell
brew install --cask xquartz
brew install ncview
```

---

#### ✅ Ubuntu / Debian 系统
大部分 Linux 系统已经自带或预装了 X11，因此直接使用 apt 安装：

```shell
sudo apt update
sudo apt install ncview
```

---

#### ✅ 其他 Linux 发行版
根据包管理器不同选择相应命令：

+ Fedora / RHEL：

```shell
sudo dnf install ncview
```

+ Arch Linux：

```shell
sudo pacman -S ncview
```

---

### 🚀 启动方式
使用终端运行以下命令，启动 ncview 可视化：

```shell
ncview your_file.nc
```

⚠️ 注意：ncview 运行依赖 GUI 环境，请确保你在图形界面下或启用了 X11 转发（如 SSH 登录时使用 `ssh -X`）。

---

### **<font style="color:rgb(38, 38, 38);">📌</font>****<font style="color:rgb(38, 38, 38);"> ncview 界面</font>**
[bandicam 2025-07-10 22-04-01-419.mp4](https://www.yuque.com/attachments/yuque/0/2025/mp4/44934637/1752156508498-0cc0af66-97d3-4c5a-acec-b5fb9bcf3949.mp4)

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752157427874-79871162-351e-41a7-9bf2-e72fcdacec09.png)

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752157463821-5631182b-4bbf-431a-b710-d2289228e1ca.png)

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752157657004-be3d186c-d993-4499-b534-9ac7a8da1763.png)

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752157766392-9ec99d64-02f0-4ed5-a93f-65340d65b96d.png)

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752157827333-8336a248-2e42-48f8-93e7-2dfaa236a7fc.png)

---

### 📦 参考材料
[netcdf数据可视化（一）](https://yizhangcug.github.io/program/2018/11/25/netcdf%E6%95%B0%E6%8D%AE%E5%8F%AF%E8%A7%86%E5%8C%96-ncview%E7%AE%80%E8%A6%81%E4%BD%BF%E7%94%A8%E8%AF%B4%E6%98%8E/#%E9%80%89%E9%A1%B9%E5%8D%A1)

---

### 🖌️ 拓展包
+ `ncmaps` 是一个为 `ncview` 增加 **更多色带（colormap）** 的扩展包。
+ `ncview` 默认只有非常有限的配色方案，颜色种类少，很多科学绘图不够直观；
+ `ncmaps` 引入了来自以下库的高质量 colormap：
    - `matplotlib`（科学绘图标准色带）
    - `cmocean`（海洋科学专用）
    - `cmcrameri`（色盲友好、科学可视化优化）

[工具推荐｜一键可视化工具ncview的强大扩展包-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/2119896)

[GitHub - TomLav/ncmaps: ncmaps brings scientific colormaps to ncview](https://github.com/TomLav/ncmaps)

---

