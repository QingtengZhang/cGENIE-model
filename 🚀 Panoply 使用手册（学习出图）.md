---

# 一、主界面
🔴 1：导入 NetCDF 文件，例如[fields_biogem_2d.zip](https://www.yuque.com/attachments/yuque/0/2025/zip/44934637/1752237993318-69fe4764-cf6d-4133-a83e-0cd519b4e753.zip)

🔴 2：清除所选的单个 NetCDF 文件

🔴 3：清除所有导入的 NetCDF 文件

🔴 4：NetCDF 文件中的变量名

🔴 5：变量更详细的、可读性更强的描述

🔴 6：用来描述数据变量的**空间维度类型，**分为 Geo1D、Geo2D、Geo3D

🔴 7：NetCDF 文件结构的详细说明

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752236345586-148547a4-0fb5-4ab9-a1ba-169b9808d696.png)

---

# 二、创建图像
:::info
+ 双击变量名即可创建图像，包含多种常用的科学图像

:::

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752238299376-9b3450f9-454a-415f-a08e-9365cbf8b747.png)

## 1. 🌍 地理参考图（Map Plots）
**适用于具有经纬度坐标的二维或三维变量**

+ **纬度-经度 图（Lat-Lon Map）**  
常见于地表变量（如温度、降水、风速等）在地图上的分布。
+ **纬度-深度 图（Lat-Vertical Map）**  
展示沿某经度切片的垂直剖面，如海洋剖面中的温度分布。
+ **经度-深度 图（Lon-Vertical Map）**  
展示沿某纬度的垂直剖面，如大气或海洋中随深度的变化。
+ **时间-纬度 图（Time-Latitude Hovmöller）**  
展示随时间变化的纬向剖面，常用于研究气候变化、季节变化等。
+ **时间-深度 图（Time-Depth Section）**  
用于显示变量在时间和垂向维度的演化。

---

## 2. 📊 通用二维变量图（Generic 2D Plots）
**适用于没有经纬度信息的二维变量**

+ 如模型输出中的任意二维数组，可按行列进行可视化。
+ 图像可以为：
    - 填色图（filled contour）
    - 轮廓图（contour lines）
    - 热力图（heatmap style）

---

## 3. 📈 折线图（Line Plots）
**适用于 1D 或 nD 变量的某个切片**

+ 单变量随时间、深度、纬度或经度的变化。
+ 支持多条线合并绘制（如不同时间或不同位置的比较）。

---

# 三、绘图控件
> 💡 Tips：以上述fields_biogem_2d.nc文件中的**<font style="color:#DF2A3F;">ocn_sur_temp</font>**变量为例
>

## 1. 数列
1.1、显示控制 (Show)

    - Arrays绘图控制 (Plot)：当前显示模式为显示数组

1.2、绘图控制 (Plot)

    - Array 1 Only：单选框，选择是否只显示第一个数组
    - Interpolate：复选框，是否对数据进行<font style="color:#DF2A3F;">插值处理</font>
    - Array 1：下拉菜单，当前选择的第一个数组是"ocn_sur_temp"

1.3、时间控制 (Year)

    - Year mid-point：年份控制
    - 当前值：`[0.500000]`（表示时间序列的中点）
    - 范围：`[ ] of 13`（表示有13个时间点，当前选择的是第1个时间点）

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752239836018-8157e964-b4aa-48f4-ba49-7c0871456dd9.png)

---

## 2. 等值线
2.1、显示模式 (Show)

    - [Contours]: 当前显示模式为等值线图

2.2、位置标记 (Locations)

    - Major scale ticks only: 仅在主要刻度位置显示等值线标签
    - 或其他样式

2.3、样式 (Style)

    - None: 不显示等值线
    - 或其他样式

2.4、颜色与线宽 (Color & Weight)

    - Color: ✔️: 启用颜色填充
    - Weight: 75%: 线宽设置为默认宽度的75%

2.5、标签设置 (Labels)

    - 💬 Visible: 标签可见
    - Size: 6.5: 标签字体大小为6.5

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752240461867-42b35815-562f-4319-a883-e8d533d394a6.png)

---

## 3. 经纬网格线
3.1、显示模式 (Show)

    - [Grid]: 当前显示模式为经纬网格

3.2、网格间距 (Spacing)

    - 15.0: 网格间距设置为15度
    - E-W X 15.0: 东西方向（经度）间隔15度
    - N-S: 南北方向（纬度）间隔15度（与经度相同）
    - 可更改为其他间距

3.3、特殊选项

    - Offset parallels from Equator: 从赤道偏移纬线（避免赤道线重叠）

3.4、线条样式 (Stroke)

    - Solid: 实线样式（可更改为其他样式）
    - Color: 默认黑色（可更改为其他样式）
    - Weight: 50%: 线宽为默认宽度的50%

3.5、标签设置 (Labels)

    - None: 不显示网格标签（可更改为其他样式）
    - Size: 6.5: 如果显示标签，字体大小为6.5磅
    - 提示: 网格标签仅适用于圆柱和伪圆柱投影（如Mercator、Robinson等）

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752240882180-6aae4430-17f0-4ff5-8e27-1f2828fe741f.png)

---

## 4. 文本标签
4.1、显示模式 (Show)

    - [Labels]: 当前显示模式为文本标签控制

4.2、标题设置 (Title & Subtitle)

    - Title: 主标题文本输入框
    - Subtitle: 副标题文本输入框

4.3、脚注设置 (Footnotes)

    - Left: 左对齐脚注内容
    - Center: 居中脚注内容
        * Show data min-max: 显示数据的最小值和最大值
        * Format: Same as scale ticks ↓: 格式与坐标轴刻度相同（可更改为其他样式）
    - Right: 右对齐脚注内容

4.4、字体设置 (Typeface)

    - SansSerif: 使用无衬线字体（可更改为其他样式）

4.5、字号设置 (Sizes)

    - Title: 16.0 ↓: 标题字号16磅（下拉箭头可能用于调整）
    - Subtitle: 12.0 ↓: 副标题字号12磅（下拉箭头可能用于调整）
    - Footnotes: 8.0 ↓: 脚注字号8磅（下拉箭头可能用于调整）

4.6、科学计数法设置 (Exponents)

    - Replace "E" notation with superscripted 10: 将科学计数法中的"E"替换为上标10（如1.2×10³代替1.2E3）

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752241321943-dbd8777d-6308-4a53-8845-33eaad59a500.png)

---

## 5. 布局控制
5.1、显示模式 (Show)

    - [Layout]: 当前显示模式为布局控制

5.2、布局元素控制

    - ☑ Include title(s): 包含标题
    - ☑ Include axes info: 包含坐标轴信息
    - ☑ Include scale colorbar: 包含比例颜色条
    - ☑ Include stroke info: 包含线条信息
    - ☑ Include footnotes: 包含脚注
    - ☑ Include standard margins: 包含标准边距

5.3、边框设置 (Border)

    - Weight: 150: 边框粗细设置为150（相对单位）

5.4、背景设置 (Background)

    - ✔️: 启用背景显示（默认应为白色）

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752241901167-1f5729e5-45b1-4db0-b4ca-36b910abf1ca.png)

---

## 6. 地图投影
6.1、显示模式 (Show)

    - [Map Projection]: 当前显示模式为地图投影控制

6.2、投影类型 (Projection)

    - Equirectangular: 当前选择的投影类型为等距圆柱投影（可更改为其他样式）

6.3、中心点设置 (Center on)

    - Lon. [0.0]° E: 中心经度设置为0.0度（可更改为其他样式）
    - Lat. [0.0]° N: 中心纬度设置为0.0度（可更改为其他样式）

6.4、标准纬线 (Std. Parallel)

    - [0.0]° N: 标准纬线设置为0.0度（可更改为其他样式）

6.5、提示信息

    - Use 'Grid' controls to manage drawing of parallels and meridians: 提示用户使用单独的"网格"控制面板管理经纬线绘制

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752242342946-17f35203-2bc5-42b3-8976-472c10be31e3.png)

---

## 7. 图层叠加
7.1、**Overlay 1 / 2 / 3**

+ Panoply 允许最多叠加 **三个图层（Overlay）**，比如边界、网格、轮廓线等。

7.2、**Name**：

+ 选择要叠加的图层类型。
    - 示例：`Earth.cno` 是一个 **地球海岸线（Coastline）** 图层文件。
    - `None` 表示不叠加图层。

7.3、**Color**：

+ 设置叠加图层的颜色。可点击方块选择颜色。

7.4、**Weight**：

+ 控制图层线条的不透明度（粗细/透明度），范围 0–100%，类似“透明度”。
    - 如 75% 表示较明显，50% 表示较浅。

7.5、**Style**：

+ 设置线条样式：
    - `Solid`：实线（默认）
    - `Dashed`：虚线
    - `Dotted`：点线
    - 等其他线条类型（依版本而异）

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752242681609-04087334-7d11-417c-87b1-46cb4b4d797c.png)

---

## 8. 比例尺
8.1、基本设置

    - Show: Scale - 显示比例尺控制

8.2、数据范围 (Range)

    - Min - 最小值
    - Max - 最大值
    - Fit to Data - 适应数据范围
    - Always fit - 总是自动适应（勾选项）

8.3、单位设置 (Units)

    - Scalar × of degrees C - 标量乘以单位
    - × 1.0 × 10^0- 缩放倍数（科学计数法）
    - Colorbar: Color Table: [ ] panoply.act - 颜色表选择
    - Reverse colors - 反转颜色

8.4、比例尺外观 (File)

    - Fill Color: 填充颜色（默认为灰色）
    - Location: Below Plot - 位置：图表下方（可改为其他位置）
    - Length: 60% - 长度占图表宽度的60%（可修改为其他样式）

8.5、离群值标记 (Outliers on)

    - Both Ends - 在两端标记离群值（可修改为其他样式）
    - Shape: Triangle - 标记形状为三角形（可修改为其他样式）
    - Gap: Thin - 与主比例尺的间隙：细缝（可修改为其他样式）

8.6、边框设置 (Border Weight)

    - 100 - 边框粗细（百分比单位）

8.7、刻度设置 (Ticks)

    - Divisions: Major: 5° - 主刻度间隔5°（可修改为其他样式）
    - Minor: 2° - 次刻度间隔2°（可修改为其他样式）

8.8、标签设置 (Labels)

    - Format: %.1f - 标签格式为保留一位小数（可修改为其他样式）
    - Size: 11.0 - 标签字体大小11磅（可修改为其他样式）

8.9、刻度长度 (Major Tick Length)

    - Short - 短刻度（可修改为其他样式）

8.10、标题设置 (Caption)

    - Default ○ Custom: SCALE CAPTION - 选择自定义标题文本
    - Size: 14.0 - 标题字体大小14磅（可修改为其他样式）

8.11、标题位置 (Location)

    - Above Colorbar - 位于颜色条上方（可修改为其他样式）

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752243067892-569e54a1-545e-4c08-90b1-c3b63553f898.png)

---

## 9. 阴影控制
9.1、显示模式 (Show)

    - [Shading]: 当前显示模式为阴影控制（昼夜分界线）

9.2、昼夜阴影选项

    - Shade nightside: 是否对夜半球进行阴影覆盖
    - Max. Darkness: 40: 最大暗度设置为40%（可修改为其他样式）
    - Subsolar Pt: Lon: -74.0° E, Lat: 23.0° N: 太阳直射点位置（西经74.0°，北纬23.0°）（可修改为其他样式）

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752243616831-4ac7a582-3fbc-4441-865d-c5ccbbc4b8e3.png)

---

## 10. 矢量图
10.1、显示模式 (Show)

    - [Vectors]: 当前显示模式为矢量图

10.2、样式设置 (Style)

    - Arrow: 使用箭头样式表示矢量（可修改为其他样式）

10.3、颜色设置 (Color)

    - 默认为黑色（可修改为其他样式）

10.4、分量方向定义

    - Array 1 values are positive East: 数组1（通常是U分量）的正值表示向东
    - Array 2 values are positive North: 数组2（通常是V分量）的正值表示向北

10.5、参考值设置

    - Reference Value: 8.474277（参考值）

10.6、比例样本显示

    - ✔ Visible: 显示比例样本（参考箭头）

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752243856280-bcd2ffd9-602a-4663-b28a-0aa24aa7edae.png)

---

# 四、参考图像
![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752244243863-01bf76e4-de7a-4e61-be4b-7eaf06fc401e.png)

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752244269544-c9246b4d-bfe0-422a-9f56-8889044019ea.png)

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752244312896-fb8a0942-2b52-4247-b51c-b7d8803d6f5c.png)![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752244318371-50aa0158-c37b-4ff4-b983-7e4876176680.png)![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752244300565-21be7fc5-bf98-4ea7-8eb6-60440458264a.png)



![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752244325545-d144374a-973f-40c6-8034-0759c8ad3c82.png)

---





