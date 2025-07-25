---

# 一、了解文件结构
[fields_biogem_2d.zip](https://www.yuque.com/attachments/yuque/0/2025/zip/44934637/1752217880114-c4f6960a-1257-4c50-9e54-a3491dc4a259.zip)

:::info
+ 运行这段代码后，控制台会输出 netCDF 文件中的维度、变量及其属性信息，帮助你了解这个数据文件的结构，方便后续的可视化或数据分析操作。需要注意，这种输出可能会很长，但它非常有助于熟悉数据内容

:::

```python
import netCDF4 as nc               # 导入 netCDF4 模块，用于读取 netCDF 文件
import matplotlib
matplotlib.use('TkAgg')           # 设置 matplotlib 使用的图形后端为 TkAgg，确保能在本地弹出窗口显示图像

# 指定你的 NetCDF 文件路径
file_path_1 = 'yourpath/fields_biogem_2d.nc'

# 打开 NetCDF 文件，以只读模式 ('r')
dataset = nc.Dataset(file_path_1, 'r')

# 打印该 NetCDF 文件的结构（包括维度、变量等信息）
print(dataset)
```

## ✅ **NetCDF 文件结构总结：**
+ **文件类型**：`NETCDF3_CLASSIC`（旧版 NetCDF 格式）
+ **说明信息**：
    - `Conventions`: CF-1.0（遵循 CF 元数据规范）
    - `title`: Time averaged integrals（时间平均积分）
    - `time_unit`: 年（Year mid-point）

---

## 📐 **维度 (Dimensions)**：
共 20 多个维度，例如：

+ `time(13)`：时间点有 13 个（不同文件的时间点可能不同）
+ `lat(36), lon(36)`：36x36 的二维地理网格
+ `zt(16)`：垂向深度层
+ 还有一些边界维度如 `lat_edges(37)`, `zt_edges(17)`，用于网格边界描述等

---

## 📊 **变量 (Variables)**：
包含数百个变量，可以大致分为以下几类（按前缀）：

1. **基础网格变量**：
    - 经纬度、深度等，如 `lat`, `lon`, `zt`, `grid_mask`, `grid_area`
2. **大气相关变量**（前缀 `atm_`）：
    - `atm_temp`, `atm_pCO2`, `atm_pO2` 等表示大气温度、气体分压等
3. **物理过程**（`phys_`）：
    - 海洋环流、风速、海冰覆盖等：`phys_psi`, `phys_wspeed`, `phys_seaice`
4. **生物地球化学通量（**`bio_`**, **`ocn_`**, **`diag_`**, **`carb_`** 等）**：
    - `ocn_int_PO4`, `bio_fexport_POC`, `carb_sur_pHsws` 等表示海洋中各种生源元素、碳酸盐系统、pH、通量等
5. **沉积与生物作用（**`biosed_`**, **`diag_int_reminP_`**, **`bio_diag_`** 等）**：
    - 描述沉积作用、有机物降解、营养盐循环等过程

---

# 二、读取二维 NetCDF 数据文件
[fields_biogem_2d.zip](https://www.yuque.com/attachments/yuque/0/2025/zip/44934637/1752217880114-c4f6960a-1257-4c50-9e54-a3491dc4a259.zip)

:::info
+  本程序旨在读取和可视化由地球系统模型（如 cGENIE）输出的二维 NetCDF 数据文件，这里以底层海水中溶解氧浓度（`ocn_ben_O2`）和海表面温度（`ocn_sur_temp`）的空间分布情况为例。该类数据通常为全球格点数据，包含纬度、经度和时间维度，并以标准 NetCDF 格式存储。通过 Python 脚本，利用 `netCDF4` 读取原始数值，配合 `Cartopy` 实现地图投影绘图，最终输出全球范围内特定时间步的海洋氧气浓度分布图和海表面温度分布图。本代码适用于古环境重建、地球化学模拟输出展示等应用场景，具有较强的通用性与可扩展性。

:::

## 🧪 例一、底层海水中溶解氧浓度
```python
# 导入必要的库
import numpy as np  # 数值计算
import netCDF4 as nc  # 读取 NetCDF 数据文件
import matplotlib
import matplotlib.pyplot as plt  # 绘图
import cartopy.crs as ccrs  # 地图投影
from matplotlib.ticker import ScalarFormatter  # 科学计数法格式设置

# 设置绘图后端（可根据系统情况进行调整）
matplotlib.use('TkAgg')  # 'TkAgg'适用于支持GUI的环境；如果报错可以注释掉

# ----------------- 全局字体设置 -----------------
# 设置整个图像的字体大小和风格，确保图像统一、美观
plt.rcParams.update({
    'font.size': 14,          # 默认字体大小
    'axes.titlesize': 16,     # 坐标轴标题字体大小
    'axes.labelsize': 14,     # 坐标轴标签字体大小
    'xtick.labelsize': 12,    # x轴刻度字体大小
    'ytick.labelsize': 12,    # y轴刻度字体大小
    'figure.titlesize': 18    # 图像标题字体大小
})

# ----------------- 数据读取部分 -----------------

# NetCDF 文件路径（根据你的文件位置自行修改）
file_path_1 = 'G:/cgenie_output/Ordovician/change-1.0O2/AP.445eb24X.PO4.0.4O2.TdepJohn2014.0.8PO4.SPIN/biogem/fields_biogem_2d.nc'

# 打开 NetCDF 文件
dataset = nc.Dataset(file_path_1, 'r')

# 读取底层海水中氧气浓度（单位一般为 mol/kg）
precip = dataset.variables['ocn_ben_O2'][:].data  # 数据维度一般是 (time, lat, lon)

# 读取纬度和经度信息
lat = dataset.variables['lat'][:]  # 纬度坐标
lon = dataset.variables['lon'][:]  # 经度坐标

# 提取并预处理数据
mylat = lat
mylon = lon
myprecip_1 = precip[12, :, :]  # 选取第13个时间步的数据（Python索引从0开始）

# 将无效数据（例如 9.96921e+36）设为 NaN，以便跳过绘制
myprecip_1[myprecip_1 == 9.9692100e+36] = np.nan

# 关闭文件，释放资源
dataset.close()

# ----------------- 绘图部分 -----------------

# 创建画布（图像窗口），尺寸为 14x8 英寸
fig = plt.figure(figsize=(14, 8))

# 设置地图投影，这里使用 Robinson 投影（全球地图常用）
ax = plt.axes(projection=ccrs.Robinson())

# 添加地图网格线（经纬度线）
gl = ax.gridlines(
    crs=ccrs.PlateCarree(),  # 使用标准平面投影画经纬线
    draw_labels=True,        # 显示标签
    linewidth=1,             # 网格线粗细
    color='lightgray',       # 网格线颜色
    alpha=0.8,               # 透明度
    linestyle='--'           # 虚线样式
)

# 只显示左侧和底部的标签
gl.top_labels = False
gl.right_labels = False

# 设置经纬度标签的字体样式
gl.xlabel_style = {'size': 22, 'color': 'k'}  # 经度标签字体大小、颜色
gl.ylabel_style = {'size': 22, 'color': 'k'}  # 纬度标签字体大小、颜色

# 绘制海底氧气浓度分布（单位转换为 μmol/kg，即1e6倍）
contour = ax.pcolormesh(
    mylon, mylat, myprecip_1 * 1e6,  # 数据乘以 1e6，单位转换为 μmol/kg
    transform=ccrs.PlateCarree(),   # 经纬度数据使用 PlateCarree 投影进行映射
    cmap='seismic',                 # 初始颜色图谱（这里会被下一行覆盖）
    shading='auto'                  # 自动选择填色方式（更平滑）
)

# 设置颜色映射为 'viridis'（会覆盖前面的 'seismic'）
contour.set_cmap('viridis')

# 添加颜色条（colorbar），显示图例
colorbar_axes = fig.add_axes([0.92, 0.2, 0.02, 0.6])  # 颜色条位置：[left, bottom, width, height]
cbar = plt.colorbar(contour, cax=colorbar_axes)  # 将颜色条放入指定位置

# 设置颜色条标签及样式
cbar.set_label('Oxygen (μmol/kg)', size=22)  # 设置单位标签（使用希腊字母μ）

# 使用科学计数法格式化颜色条
cbar.formatter = ScalarFormatter(useMathText=True)  # 使用科学计数
cbar.formatter.set_powerlimits((-3, 3))  # 设置指数范围
cbar.update_ticks()  # 更新刻度

# 设置颜色条刻度字体大小
cbar.ax.tick_params(labelsize=22)

# 保存图像为 PNG 文件
plt.savefig('1.png',
            bbox_inches='tight',  # 去除多余白边
            dpi=300,              # 分辨率 300 dpi（高清）
            facecolor='white')    # 背景为白色

# 显示图像
plt.show()
```

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752220683815-9b6f7202-af05-41de-b524-34e078008e47.png)

## 🧪 例二、海表面温度
```python
# 引入所需的第三方库
import numpy as np                      # 用于数值计算与数组处理
import netCDF4 as nc                   # 用于读取 .nc 文件（NetCDF 格式）
import matplotlib                      # matplotlib 主模块，用于设置图像后端
import matplotlib.pyplot as plt        # pyplot 是 matplotlib 的绘图接口
import cartopy.crs as ccrs             # Cartopy 地图投影库，用于绘制地图
from matplotlib.ticker import ScalarFormatter  # 用于控制颜色条的刻度格式（科学计数法）

# 设置 matplotlib 使用的图形后端（可选）
matplotlib.use('TkAgg')  # 如果你在某些系统上遇到绘图卡住问题，可以注释或更改此行

# ----------------- 全局字体设置 -----------------
# 统一设置图像中文字的大小，增强图像的一致性与可读性
plt.rcParams.update({
    'font.size': 14,          # 默认字体大小
    'axes.titlesize': 16,     # 图像子图标题的字体大小
    'axes.labelsize': 14,     # 坐标轴标签的字体大小
    'xtick.labelsize': 12,    # x轴刻度字体大小
    'ytick.labelsize': 12,    # y轴刻度字体大小
    'figure.titlesize': 18    # 整张图的主标题字体大小
})

# ----------------- 数据读取部分 -----------------
# 指定 NetCDF 数据文件路径（改为你实际的数据路径）
file_path_1 = 'G:/cgenie_output/Ordovician/change-0.4O2/AP.445eb24X.PO4.0.4O2.TdepJohn2014.0.4PO4.SPIN/biogem/fields_biogem_2d.nc'

# 打开 NetCDF 文件，读取内容
dataset = nc.Dataset(file_path_1, 'r')

# 提取变量：
# 这里读取的是表层海水温度（单位：摄氏度），形状为 (time, lat, lon)
precip = dataset.variables['ocn_sur_temp'][:].data

# 读取经纬度
lat = dataset.variables['lat'][:]
lon = dataset.variables['lon'][:]

# 处理数据
mylat = lat                    # 纬度数组
mylon = lon                   # 经度数组
myprecip_1 = precip[12, :, :] # 提取第13个时间步（索引从0开始）对应的温度场数据

# 将缺失值替换为 NaN（通常 NetCDF 中用 9.969e+36 表示缺失）
myprecip_1[myprecip_1 == 9.9692100e+36] = np.nan

# 关闭 NetCDF 文件
dataset.close()

# ----------------- 绘图部分 -----------------
# 创建图像窗口，设置画布大小
fig = plt.figure(figsize=(14, 8))  # 单位是英寸

# 创建地图投影轴（Robinson 投影适合全球可视化）
ax = plt.axes(projection=ccrs.Robinson())

# ----------------- 网格线设置 -----------------
gl = ax.gridlines(
    crs=ccrs.PlateCarree(),      # 使用等经纬度网格来画刻度
    draw_labels=True,            # 显示坐标轴刻度标签
    linewidth=1,
    color='lightgray',
    alpha=0.8,
    linestyle='--'
)
gl.top_labels = False            # 不显示顶部刻度标签
gl.right_labels = False          # 不显示右侧刻度标签

# 设置经纬度刻度标签的字体样式
gl.xlabel_style = {'size': 22, 'color': 'k'}  # 经度标签字体设置
gl.ylabel_style = {'size': 22, 'color': 'k'}  # 纬度标签字体设置

# ----------------- 绘制数据 -----------------
# 将温度数据绘制在地图上，使用经纬度为坐标
contour = ax.pcolormesh(
    mylon, mylat, myprecip_1,              # 经度、纬度、温度值
    transform=ccrs.PlateCarree(),          # 指定数据坐标系为经纬度
    cmap='seismic',                        # 配色方案，可更改为其他，如 viridis、coolwarm
    shading='auto'                         # 自动选择栅格填充方式
)

# ----------------- 颜色条设置 -----------------
# 在图像右侧添加颜色条（colorbar），单独创建颜色条轴
colorbar_axes = fig.add_axes([0.92, 0.2, 0.02, 0.6])  # [left, bottom, width, height]
cbar = plt.colorbar(contour, cax=colorbar_axes)      # 将颜色条绑定到绘图对象
cbar.set_label('Sea Surface Temperature (℃)', size=22)  # 设置颜色条标题，单位为摄氏度

# ----------------- 颜色条格式设置 -----------------
# 使用科学计数法显示颜色条刻度（如 1e1、1e2 等）
cbar.formatter = ScalarFormatter(useMathText=True)
cbar.formatter.set_powerlimits((-3, 3))  # 设置何时采用科学记数法
cbar.update_ticks()                     # 应用设置

# 设置颜色条刻度字体大小
cbar.ax.tick_params(labelsize=22)

# ----------------- 保存并展示图像 -----------------
plt.savefig('1.png',            # 输出文件名
           bbox_inches='tight', # 去除边缘空白
           dpi=300,             # 图像分辨率（适合论文）
           facecolor='white')   # 背景颜色
plt.show()                      # 显示图像
```

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752220721152-39267b2d-a00c-468d-884d-0b999e034fec.png)

## 🧪 例三、DIY不同用途的程序（持续更新）
:::info
+  这段代码用于分析古气候模拟数据中海底氧含量的空间分布情况，通过统计氧含量小于等于零的格点在所有有效海底格点中的占比，量化缺氧或无氧区域的面积比例，为研究古海洋缺氧事件（如海洋缺氧带扩展）提供量化依据，有助于理解过去环境变化对海洋生态系统的影响。

:::

```python
# 导入必要的库
import numpy as np  # 数值计算
import netCDF4 as nc  # 读取 NetCDF 数据文件
import matplotlib
import matplotlib.pyplot as plt  # 绘图
import cartopy.crs as ccrs  # 地图投影
from matplotlib.ticker import ScalarFormatter  # 科学计数法格式设置

# 设置绘图后端（可根据系统情况进行调整）
matplotlib.use('TkAgg')  # 'TkAgg'适用于支持GUI的环境；如果报错可以注释掉

# ----------------- 全局字体设置 -----------------
# 设置整个图像的字体大小和风格，确保图像统一、美观
plt.rcParams.update({
    'font.size': 14,          # 默认字体大小
    'axes.titlesize': 16,     # 坐标轴标题字体大小
    'axes.labelsize': 14,     # 坐标轴标签字体大小
    'xtick.labelsize': 12,    # x轴刻度字体大小
    'ytick.labelsize': 12,    # y轴刻度字体大小
    'figure.titlesize': 18    # 图像标题字体大小
})

# ----------------- 数据读取部分 -----------------

# NetCDF 文件路径（根据你的文件位置自行修改）
file_path_1 = 'G:/cgenie_output/Ordovician/change-1.0O2/AP.445eb24X.PO4.0.4O2.TdepJohn2014.0.8PO4.SPIN/biogem/fields_biogem_2d.nc'

# 打开 NetCDF 文件
dataset = nc.Dataset(file_path_1, 'r')

# 读取底层海水中氧气浓度（单位一般为 mol/kg）
precip = dataset.variables['ocn_ben_O2'][:].data  # 数据维度一般是 (time, lat, lon)

# 读取纬度和经度信息
lat = dataset.variables['lat'][:]  # 纬度坐标
lon = dataset.variables['lon'][:]  # 经度坐标

# 提取并预处理数据
mylat = lat
mylon = lon
myprecip_1 = precip[12, :, :]  # 选取第13个时间步的数据（Python索引从0开始）

# 将无效数据（例如 9.96921e+36）设为 NaN，以便跳过绘制
myprecip_1[myprecip_1 == 9.9692100e+36] = np.nan

# 关闭文件，释放资源
dataset.close()

# ----------------- 绘图部分 -----------------

# 创建画布（图像窗口），尺寸为 14x8 英寸
fig = plt.figure(figsize=(14, 8))

# 设置地图投影，这里使用 Robinson 投影（全球地图常用）
ax = plt.axes(projection=ccrs.Robinson())

# 添加地图网格线（经纬度线）
gl = ax.gridlines(
    crs=ccrs.PlateCarree(),  # 使用标准平面投影画经纬线
    draw_labels=True,        # 显示标签
    linewidth=1,             # 网格线粗细
    color='lightgray',       # 网格线颜色
    alpha=0.8,               # 透明度
    linestyle='--'           # 虚线样式
)

# 只显示左侧和底部的标签
gl.top_labels = False
gl.right_labels = False

# 设置经纬度标签的字体样式
gl.xlabel_style = {'size': 22, 'color': 'k'}  # 经度标签字体大小、颜色
gl.ylabel_style = {'size': 22, 'color': 'k'}  # 纬度标签字体大小、颜色

# 绘制海底氧气浓度分布（单位转换为 μmol/kg，即1e6倍）
contour = ax.pcolormesh(
    mylon, mylat, myprecip_1 * 1e6,  # 数据乘以 1e6，单位转换为 μmol/kg
    transform=ccrs.PlateCarree(),   # 经纬度数据使用 PlateCarree 投影进行映射
    cmap='seismic',                 # 初始颜色图谱（这里会被下一行覆盖）
    shading='auto'                  # 自动选择填色方式（更平滑）
)

# 设置颜色映射为 'viridis'（会覆盖前面的 'seismic'）
contour.set_cmap('viridis')

# 添加颜色条（colorbar），显示图例
colorbar_axes = fig.add_axes([0.92, 0.2, 0.02, 0.6])  # 颜色条位置：[left, bottom, width, height]
cbar = plt.colorbar(contour, cax=colorbar_axes)  # 将颜色条放入指定位置

# 设置颜色条标签及样式
cbar.set_label('Oxygen (μmol/kg)', size=22)  # 设置单位标签（使用希腊字母μ）

# 使用科学计数法格式化颜色条
cbar.formatter = ScalarFormatter(useMathText=True)  # 使用科学计数
cbar.formatter.set_powerlimits((-3, 3))  # 设置指数范围
cbar.update_ticks()  # 更新刻度

# 设置颜色条刻度字体大小
cbar.ax.tick_params(labelsize=22)

# 保存图像为 PNG 文件
plt.savefig('1.png',
            bbox_inches='tight',  # 去除多余白边
            dpi=300,              # 分辨率 300 dpi（高清）
            facecolor='white')    # 背景为白色

# 显示图像
plt.show()

# ---------------------------- 计算氧含量小于等于0区域所占海底比例 ----------------------------

# 去除无效值（NaN），保留真实有效的海底氧含量数据
valid_data = myprecip_1[~np.isnan(myprecip_1)]  # 提取所有非 NaN 的数据（表示有数据覆盖的海底区域）

# 统计氧含量小于等于 0 的网格数（即严重缺氧或无氧区域）
count_leq_zero = np.sum(valid_data <= 0)

# 统计总的有效网格数（即有观测或模拟值的海底格点数）
count_valid = len(valid_data)

# 计算无氧区域占比（百分比表示）
percentage_leq_zero = (count_leq_zero / count_valid) * 100

# 输出结果，保留两位小数
print(f"海底氧含量小于等于0的区域占比: {percentage_leq_zero:.2f}%")
```

---

# 三、读取三维 NetCDF 数据文件
[fields_biogem_3d.zip](https://www.yuque.com/attachments/yuque/0/2025/zip/44934637/1752221288144-6cb450a1-dfd1-4b74-b712-d56fc2970b97.zip)

:::info
+   二维 NetCDF 文件主要用于描述随时间变化的地表变量，其数据通常为三维结构 `(time, lat, lon)`，如海表温度（SST）或海表氧气浓度。而三维 NetCDF 文件在此基础上加入了垂向维度 `zt`（代表海洋深度层），形成四维结构 `(time, zt, lat, lon)`。这使得用户能够提取任意时间、任意深度的空间剖面信息，更全面地分析三维海洋环境结构，如温度、盐度、养分和氧气在不同深度的分布，广泛应用于古海洋模拟、气候变化重建等地球系统科学研究中。  

:::

```python
import numpy as np
import netCDF4 as nc
import matplotlib.pyplot as plt
import cartopy.crs as ccrs
from matplotlib.ticker import ScalarFormatter

# NetCDF 文件路径（根据你的文件位置自行修改）
file_path = 'G:/cgenie_output/Ordovician/change-0.4O2/AP.445eb24X.PO4.0.4O2.TdepJohn2014.0.4PO4.SPIN/biogem/fields_biogem_3d.nc'
dataset = nc.Dataset(file_path, 'r')

# 提取变量
temp = dataset.variables['ocn_temp'][:]    # 4D: time, zt, lat, lon
lat = dataset.variables['lat'][:]
lon = dataset.variables['lon'][:]
zt = dataset.variables['zt'][:]            # 垂向层数组（深度单位为 m）

# ---------------------- 设置参数 ----------------------
time_index = 12   # 第13个时间步
num_layers = 16   # 读取前16个zt层
cmap = 'seismic'  # 色图样式

# 统一色标范围（全层取最大最小）
temp_selected = temp[time_index, :num_layers, :, :]
temp_selected[temp_selected == 9.9692100e+36] = np.nan
vmin = np.nanmin(temp_selected)
vmax = np.nanmax(temp_selected)

# ---------------------- 创建大图（4×4 子图） ----------------------
fig, axes = plt.subplots(
    nrows=4,
    ncols=4,
    figsize=(20, 12),
    subplot_kw={'projection': ccrs.Robinson()}
)

fig.suptitle('Temperature Distribution at Different Depth Layers (zt)', fontsize=20)

# 遍历每一层
for i in range(num_layers):
    ax = axes[i // 4, i % 4]
    data = temp[time_index, i, :, :]
    data[data == 9.9692100e+36] = np.nan

    # 绘图
    mesh = ax.pcolormesh(
        lon, lat, data,
        transform=ccrs.PlateCarree(),
        cmap=cmap,
        shading='auto',
        vmin=vmin,
        vmax=vmax
    )

    ax.set_title(f"zt = {zt[i]:.1f} m", fontsize=12)
    ax.set_global()
    ax.gridlines(draw_labels=False, linewidth=0.5, linestyle='--', color='gray')

# ---------------------- 添加统一颜色条 ----------------------
cbar_ax = fig.add_axes([0.92, 0.2, 0.015, 0.6])
cbar = fig.colorbar(mesh, cax=cbar_ax)
cbar.set_label('Temperature (℃)', fontsize=16)
cbar.formatter = ScalarFormatter(useMathText=True)
cbar.formatter.set_powerlimits((-3, 3))
cbar.update_ticks()
cbar.ax.tick_params(labelsize=14)

# ---------------------- 保存与显示 ----------------------
plt.subplots_adjust(wspace=0.05, hspace=0.2, right=0.9)
plt.savefig('temperature_16layers.png', dpi=300, bbox_inches='tight', facecolor='white')
plt.show()

dataset.close()
```

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752222094858-8aceb57f-7185-4cda-abda-fc2eaaab88e9.png)

---

# 四、**NetCDF 文件间的**数值计算
[31texyga.pdclann.zip](https://www.yuque.com/attachments/yuque/0/2025/zip/44934637/1752223344430-49b33587-1f60-430a-acd4-64d04bf28774.zip)

[36texyha.pdclann.zip](https://www.yuque.com/attachments/yuque/0/2025/zip/44934637/1752223349363-c391caa1-6f0f-4186-bc14-1ebf137706ff.zip)

:::info
+ NetCDF 文件间的数值计算通常用于比较或分析不同数据集之间的变化或差异。以差值计算为例，首先需要确保两个数据集在空间和时间维度上具有相同的格点和结构，然后读取对应变量的数据，对应位置的数值进行逐点相减，得到新的差异数据集。这种方法广泛应用于气象、海洋和环境科学中，用于评估模型模拟结果的变化、观测数据的对比或不同情景下的变量差异。

:::

```python
import numpy as np
import netCDF4 as nc
import matplotlib.pyplot as plt
import matplotlib.colors as mcolors
import cartopy.crs as ccrs
import matplotlib
from matplotlib.ticker import ScalarFormatter

# 设置后端（如无GUI可注释）
matplotlib.use('TkAgg')

# 设置字体样式
plt.rcParams.update({
    'font.size': 14,           # 基础字体大小
    'axes.titlesize': 16,      # 标题大小
    'axes.labelsize': 14,      # 坐标轴标签大小
    'xtick.labelsize': 12,     # X轴刻度
    'ytick.labelsize': 12,     # Y轴刻度
    'figure.titlesize': 18     # 图形标题
})

# ------------------- 数据读取 -------------------
# NetCDF 文件路径（根据你的文件位置自行修改）
file_path_1 = 'D:/python_project/pythonProject1/31texyga.pdclann.nc'
file_path_2 = 'D:/python_project/pythonProject1/36texyha.pdclann.nc'

# 打开第一个数据集
ds1 = nc.Dataset(file_path_1)
temp1 = ds1.variables['temp_mm_1_5m'][:].data[0, 0, :, :]
lat = ds1.variables['latitude'][:]
lon = ds1.variables['longitude'][:]
ds1.close()

# 打开第二个数据集
ds2 = nc.Dataset(file_path_2)
temp2 = ds2.variables['temp_mm_1_5m'][:].data[0, 0, :, :]
ds2.close()

# 计算温度差异
temp_diff = temp1 - temp2

# 计算颜色条范围（使0居中）
abs_max = np.nanmax(np.abs(temp_diff))
vmin, vmax = -abs_max, abs_max

# ------------------- 绘图 -------------------
fig = plt.figure(figsize=(14, 7))
ax = plt.axes(projection=ccrs.Robinson())  # 使用Robinson投影

# 使用红蓝色图，强调正负差异
cmap = plt.get_cmap('RdBu_r')
im = ax.pcolormesh(
    lon, lat, temp_diff,
    cmap=cmap,
    shading='auto',
    vmin=vmin,
    vmax=vmax,
    transform=ccrs.PlateCarree()
)

# 设置颜色条
cbar = plt.colorbar(im, ax=ax, orientation='vertical', shrink=0.6, pad=0.05)
cbar.set_label('Temperature Difference (°C)', fontsize=16)
cbar.formatter = ScalarFormatter(useMathText=True)
cbar.formatter.set_powerlimits((-3, 3))
cbar.update_ticks()
cbar.ax.tick_params(labelsize=14)

# 设置标题
plt.title('Temperature Difference Between Two Datasets (°C)', fontsize=18)

# 可选：加网格线
ax.gridlines(draw_labels=False, linewidth=0.5, linestyle='--', color='gray')

# 保存与显示
plt.savefig('temp_difference_robinson.png', dpi=300, bbox_inches='tight', facecolor='white')
plt.show()
```

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752226687278-7eaa0bbb-2ac3-4e26-9620-2efdc0b7a869.png)

---

# 五、**xarray与netCDF4-python有什么区别？**
> 💡 Tips：`xarray` 和 `netCDF4-python` 都是用于处理 NetCDF 数据的 Python 库，但它们在**<font style="color:#DF2A3F;">功能层级、使用体验和设计理念</font>****<font style="color:#DF2A3F;">上存在明显区别</font>**，以下是使用 `xarray` 重写的代码，并附有与 `netCDF4-python` 版本的对比分析：
>

```python
import xarray as xr
import matplotlib.pyplot as plt
import matplotlib.colors as mcolors
import cartopy.crs as ccrs
import matplotlib
import numpy as np

# 设置后端（根据实际需要选择）
matplotlib.use('TkAgg')  # 可选，如果遇到GUI问题可以注释掉

from matplotlib.ticker import ScalarFormatter

# 设置字体样式
plt.rcParams.update({
    'font.size': 14,           # 基础字体大小
    'axes.titlesize': 16,      # 标题大小
    'axes.labelsize': 14,      # 坐标轴标签大小
    'xtick.labelsize': 12,     # X轴刻度
    'ytick.labelsize': 12,     # Y轴刻度
    'figure.titlesize': 18     # 图形标题
})

# ------------------- 数据读取 -------------------
# NetCDF 文件路径（根据你的文件位置自行修改）
file_path_1 = 'D:/python_project/pythonProject1/31texyga.pdclann.nc'
file_path_2 = 'D:/python_project/pythonProject1/36texyha.pdclann.nc'

# 使用xarray打开数据集（自动管理资源）
ds1 = xr.open_dataset(file_path_1, decode_times=False)
ds2 = xr.open_dataset(file_path_2, decode_times=False)

# 使用xarray的标签索引选择数据
temp1 = ds1['temp_mm_1_5m'].isel(t=0, ht=0)  # 使用维度名称索引
temp2 = ds2['temp_mm_1_5m'].isel(t=0, ht=0)  # 避免硬编码索引位置

# 计算温度差异（xarray自动处理元数据）
temp_diff = temp1 - temp2

# ------------------- 绘图 -------------------
fig = plt.figure(figsize=(14, 7))
ax = plt.axes(projection=ccrs.Robinson())

# 使用xarray的绘图集成（更简洁的语法）
im = temp_diff.plot.pcolormesh(
    ax=ax,
    cmap='RdBu_r',
    add_colorbar=False,  # 手动添加颜色条以获得更多控制
    shading='auto',
    transform=ccrs.PlateCarree()
)

# 设置颜色条
cbar = plt.colorbar(im, ax=ax, orientation='vertical', shrink=0.6, pad=0.05)
cbar.set_label('Temperature Difference (°C)', fontsize=16)
cbar.formatter = ScalarFormatter(useMathText=True)
cbar.formatter.set_powerlimits((-3, 3))
cbar.update_ticks()
cbar.ax.tick_params(labelsize=14)

# 设置标题
plt.title('Temperature Difference Between Two Datasets (°C)', fontsize=18)

ax.gridlines(draw_labels=False, linewidth=0.5, linestyle='--', color='gray')

# 保存与显示
plt.savefig('temp_difference_robinson_xarray.png', dpi=300, bbox_inches='tight', facecolor='white')
plt.show()

# 关闭数据集（可选，xarray在with语句中自动处理）
ds1.close()
ds2.close()
```

## 📦 主要区别分析：
1. **数据访问方式**
    - `netCDF4-python`：需要手动提取变量和维度

```python
temp1 = ds1.variables['temp_mm_1_5m'][:].data[0, 0, :, :]
lat = ds1.variables['latitude'][:]
lon = ds1.variables['longitude'][:]
```

    - `xarray`：使用维度名称进行索引

```python
temp1 = ds1['temp_mm_1_5m'].isel(t=0, ht=0)
```

2. **数据操作**
    - `netCDF4-python`：直接操作NumPy数组

```python
temp_diff = temp1 - temp2  # 纯NumPy操作
```

    - `xarray`：保留元数据的算术运算

```python
temp_diff = temp1 - temp2  # 自动保留坐标和属性
```

3. **绘图集成**
    - `netCDF4-python`：需要手动设置绘图参数

```python
im = ax.pcolormesh(lon, lat, temp_diff, ...)
```

    - `xarray`：内置绘图方法

```python
im = temp_diff.plot.pcolormesh(ax=ax, ...)
```

4. **资源管理**
    - `netCDF4-python`：需要显式关闭文件

```python
ds1.close()
ds2.close()
```

    - `xarray`：推荐使用上下文管理器自动关闭

```python
with xr.open_dataset(...) as ds:
    # 处理数据
```

5. **元数据处理**
    - `netCDF4-python`：需要手动处理单位、填充值等
    - `xarray`：自动处理单位转换和缺失值

```python
# 自动处理单位（示例）
if 'units' in temp1.attrs and temp1.attrs['units'] == 'K':
    temp1 = temp1 - 273.15  # 转换为摄氏度
```

## 📦 关键优势对比：
| 特性 | `netCDF4-python` | `xarray` |
| --- | --- | --- |
| **维度处理** | 需要手动管理索引 | 支持维度名称索引 |
| **元数据保留** | 算术运算丢失元数据 | 自动保留坐标和属性 |
| **绘图集成** | 需要手动设置 | 内置高级绘图方法 |
| **时间处理** | 返回原始数值 | 自动转换为datetime对象 |
| **大文件支持** | 有限 | 支持Dask分块处理 |
| **坐标感知** | 无 | 支持基于坐标的选择（如`sel(lat=40)`） |


## 📦 推荐使用场景：
1. **使用**`xarray`**当**：
    - 需要基于坐标选择数据（如`sel(time='2020-01-01')`）
    - 处理多维数据集时保持元数据
    - 需要集成Dask进行并行计算
    - 进行复杂的时间序列分析
2. **使用**`netCDF4-python`**当**：
    - 需要直接操作底层NetCDF结构
    - 处理非标准NetCDF文件格式
    - 进行低级文件操作（如修改文件结构）
    - 在资源受限环境中需要最小依赖

[GitHub - pydata/xarray: N-D labeled arrays and datasets in Python](https://github.com/pydata/xarray)

---

