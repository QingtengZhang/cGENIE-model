> 💡 Tips：Panoply 是由 NASA GISS 开发的跨平台 NetCDF、HDF、GRIB 等科学数据可视化工具，适合处理大气、海洋、气候模型等网格数据。
>

---

## 📌 基本信息
+ 当前版本：**5.6.1**
+ 发布日期：**2025-05-08**
+ 运行需求：需安装 **Java 11 或更高版本**
+ 官网地址：[https://www.giss.nasa.gov/tools/panoply/](https://www.giss.nasa.gov/tools/panoply/)

---

## 📊 Panoply 5 的功能
:::info
+ 创建具有颜色等高线的地理参考图，包括以下维度的切片：纬度-经度、纬度-垂直、经度-垂直、时间-纬度 或 时间-垂直，来源于二维或更高维度的变量。
+ 创建“通用”二维数组的颜色等高线图，来源于二维或更高维度的变量。
+ 创建来自一维或更高维度变量的数据折线图。
+ 将两个地理参照数组合并到一张图中，通过做差、求和或取平均的方式。
+ 基于 CF 规范或类似格式，绘制轨迹数据的地图图。
+ 使用超过 200 种地图投影中的任意一种，在全球或区域地图上绘制经纬度数据，或制作纬向平均折线图。
+ 在经纬度地图图上叠加大陆轮廓或遮罩图。
+ 为比例尺颜色条使用任意数量的颜色表，或应用您自定义的 ACT、CPT 或 RGB 颜色表。
+ 将图像保存为磁盘中的 GIF、JPEG、PNG 或 TIFF 位图图像，或以 PDF、PostScript 或 SVG 矢量图形文件格式保存。
+ 以 KMZ 格式导出经纬度地图图。
+ 打开存储在 HTTP/HTTPS 网站或 S3 桶中的远程 netCDF 和 HDF 数据集。
+ 浏览远程 THREDDS 和 OPeNDAP 目录，并打开由它们提供的数据集。
+ 将动画导出为 MP4 视频，或作为单独帧图像的集合导出。

:::

---

## 💾 下载地址（v5.6.1）
### 📱 macOS
| 类型 | 下载包 | 说明 |
| --- | --- | --- |
| Apple Silicon (ARM64) | 48 MB DMG | 适用于 M 系列芯片（M1/M2/M3 等） |
| Intel + 原生文件选择器 | 48 MB DMG | 老款 Intel 芯片，使用 macOS 原生文件选择器 |
| Intel + Java 文件选择器（JFC） | 48 MB DMG | 解决多屏幕下文件选择器无响应问题 |


### 🖥 Windows
| 类型 | 下载包 | 说明 |
| --- | --- | --- |
| 通用版本 | 45 MB ZIP | 必须先解压再运行，否则会加载错误 |


### 🐧 Linux / 其他系统
| 类型 | 下载包 | 说明 |
| --- | --- | --- |
| 通用 ZIP 包 | 45 MB ZIP | 手动解压即可使用 |
| 通用 TGZ 包 | 45 MB TGZ | 使用 `tar` 解压时可能出现警告，可忽略 |


👉 [前往官网下载页](https://www.giss.nasa.gov/tools/panoply/download/)

---

## 🚀 安装与运行说明
### macOS 用户注意事项
+ 需安装 **Java 11+**。若无，请参考压缩包内的 `README_JAVA11`，使用推荐的开源 Java 实现（如 Adoptium）。
+ Apple Silicon 用户需确保安装 ARM64 架构的 Java。
+ Intel Mac 多屏幕下文件选择器失灵时，请使用 **JFC 版本**。
+ Magic Mouse 有时会导致点击无响应，属 macOS 和 Java 的兼容性问题。

### Windows 用户说明
+ 请务必将 ZIP 压缩包**解压**后再运行。
+ Java 需正确配置注册表项。某些 Java 发行版不会自动配置，需手动设置（见 `README_JAVA11`）。

### Linux 用户说明
+ 推荐使用 `tar -xzf` 解压 TGZ 包。
+ 解压时出现 `Ignoring unknown extended header keyword` 属正常情况，可忽略。
+ 启动方法（假设在解压目录内）：

```bash
./panoply.sh
```

---

## 🎨 颜色表与地图叠加
Panoply 内置一组标准的颜色表和地图轮廓线，但你也可以添加自定义内容：

+ ✅ 可加载 SHP 矢量地图（注意不支持含 `.prj` 投影文件的 shapefile）
+ ✅ 可从以下资源获取更多色标：
    - [cpt-city](http://soliton.vm.bytemark.co.uk/pub/cpt-city/)：提供大量 CPT 格式颜色表
    - [NCL Color Gallery](https://www.ncl.ucar.edu/Document/Graphics/color_table_gallery.shtml)

---

## ⚠ 常见问题及解决方案
| 问题 | 可能原因 / 解决方式 |
| --- | --- |
| Panoply 无法启动 | Java 未安装或版本低于 11 |
| 打开 ZIP 后直接双击 Panoply 图标时报错 | 必须解压后运行（Windows） |
| 多显示器下文件选择器失灵 | 使用 macOS Intel + JFC 版本 |
| 鼠标点击无响应 | Magic Mouse + macOS Java 问题 |
| 色标加载失败 | 检查格式，确保为 Panoply 支持的 CPT 或 RGB 格式 |


---

## ⚠️ Java 11 安装须知（Windows）
+ 如果你的计算机尚未安装 **Java 11 或更高版本**，尝试启动 Panoply 时，可能会弹出对话框提示你需要安装 Java 11。
+ 但即使已经安装了 Java 11，**若 Panoply.exe 启动器无法定位 Java 的安装路径**，也会显示同样的提示。这通常发生在使用了非 Oracle 的开源 Java 发行版（例如 Temurin、Corretto、Zulu 等）但它们**没有将 Java 安装路径写入 Windows 注册表**时。
+ 在没有注册表信息的情况下，Panoply.exe 也会尝试使用 `%JAVA_HOME%` 环境变量来查找 Java。如果该路径下的 Java 版本不是 Java 11 或更高，Panoply 启动可能会**崩溃且无任何提示**。

---

## ✅ 推荐的 Java 安装方式（以 Temurin 为例）
Panoply 用户报告，使用 **Adoptium 的 Temurin 发行版** 效果良好：  
🔗 [https://adoptium.net/](https://adoptium.net/)

在安装 Temurin 时：

1. 安装向导中会显示名为 **“Custom Setup”** 的面板；
2. 在此面板中，务必手动启用以下两个选项（默认是未启用的）：
    - ✅ **Set JAVA****_****HOME variable**
    - ✅ **JavaSoft registry keys**

否则，Panoply 启动器仍可能无法找到 Java。

---

## 📘 附录
+ 官方文档：压缩包内含 `README.txt` 和 `README_JAVA11.txt`
+ 验证包完整性：官网[MD5] [SHA1] [SHA256] 校验值已提供
+ 示例数据： 可从 NASA 等机构获取 `.nc`, `.hdf`, `.grib` 文件测试  

---

