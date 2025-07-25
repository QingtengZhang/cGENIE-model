---

# 🧱 Blender 是什么？
**Blender** 是一个免费开源、跨平台的 **3D 建模和动画制作软件**，功能强大，广泛应用于：

+ 🎬 影视动画制作（建模、渲染、角色绑定、动画、特效等）
+ 🕹️ 游戏开发（导出模型、动画）
+ 🧪 科学可视化（模拟与数据展示）
+ 📐 工业建模与设计（原型展示、可视分析）

Blender 拥有内置的脚本引擎（Python API），可以让用户 **二次开发** 或构建自定义插件/工具。

---

# 🌊 BlenderNC 是什么？
**BlenderNC（Blender for NetCDF）** 是一个 Blender 插件，用于将 **科学数据（尤其是 netCDF 文件）** 可视化成高质量图像/动画。

它主要服务于：

+ 🌍 气候科学
+ 🌊 海洋学
+ ☁️ 气象研究
+ 🌡️ 地球系统模拟数据的展示

## ✨ 核心功能：
+ 支持读取 **NetCDF 数据（.nc 文件）**
+ 可自动映射数据到 **纹理贴图**，生成动态动画
+ 支持时间序列动画（比如风速、温度、海流等随时间变化的可视化）
+ 与 Blender 的材质、光照、动画系统无缝集成

> 💡 Tips：**<font style="color:#DF2A3F;background-color:rgb(252, 252, 252);">Blender 功能强大但上手较难，对电脑配置要求较高，尤其在渲染和大数据可视化时更明显</font>**
>

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752212737580-edeec5b2-b1d3-4ab9-a20f-dbf3606db818.png)

---

# **<font style="color:rgb(38, 38, 38);">📚</font>****<font style="color:rgb(38, 38, 38);"> 操作手册</font>**
## <font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">BlenderNC</font>
**<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">BlenderNC</font>**<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);"> </font><font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">is a Blender add-on that allows importing datacubes into Blender (i.e. netCDF, cfGrib, and zarr files). It allows 2D and 3D visualization and the generation of scientific data animations. The main development of</font><font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);"> </font>_<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">BlenderNC</font>_<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);"> </font><font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">currently focuses on geo-spatial data (i.e. Oceanographic - Atmospheric data), however, the framework should support the load of any datacube.</font>

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752211920140-be6ee38b-9e54-4d5e-9559-b6058ab9796a.png)

## **<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">Quick Start</font>**
+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Install BlenderNC</font>](https://blendernc.readthedocs.io/en/docs/install.html)
    - [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Setting up the Blender Python environment</font>](https://blendernc.readthedocs.io/en/docs/install.html#setting-up-the-blender-python-environment)
    - [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Install Addon</font>](https://blendernc.readthedocs.io/en/docs/install.html#install-addon)
    - [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Update BlenderNC</font>](https://blendernc.readthedocs.io/en/docs/install.html#update-blendernc)
    - [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Blender Compilation (optional)</font>](https://blendernc.readthedocs.io/en/docs/install.html#blender-compilation-optional)
+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">How to use BlenderNC</font>](https://blendernc.readthedocs.io/en/docs/howtouse.html)
    - [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Beginner mode!</font>](https://blendernc.readthedocs.io/en/docs/beginner_mode.html)
    - [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">PRO mode!</font>](https://blendernc.readthedocs.io/en/docs/pro_mode.html)
    - [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Helpful videos</font>](https://blendernc.readthedocs.io/en/docs/extra/blender_support_videos.html)
+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">BlenderNC Preferences</font>](https://blendernc.readthedocs.io/en/docs/preferences.html)
    - [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Workspace</font>](https://blendernc.readthedocs.io/en/docs/preferences.html#workspace)
    - [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Shading</font>](https://blendernc.readthedocs.io/en/docs/preferences.html#shading)
+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Remote rendering</font>](https://blendernc.readthedocs.io/en/docs/remote_render.html)
    - [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Background render tutorial</font>](https://blendernc.readthedocs.io/en/docs/background.html)
    - [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Gadi</font>](https://blendernc.readthedocs.io/en/docs/nci.html)
    - [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">VDI</font>](https://blendernc.readthedocs.io/en/docs/nci.html#vdi)

## **<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">Examples</font>**
+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Import Gebco Topography</font>](https://blendernc.readthedocs.io/en/docs/examples/import_gebco_netCDF.html)
+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Simple animation</font>](https://blendernc.readthedocs.io/en/docs/examples/simple_animation.html)
+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Import ECMWF netCDF</font>](https://blendernc.readthedocs.io/en/docs/examples/import_ECMWF_netCDF.html)
+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Import ECMWF GRIB</font>](https://blendernc.readthedocs.io/en/docs/examples/import_ECMWF_grib.html)
+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Displacement rendering</font>](https://blendernc.readthedocs.io/en/docs/examples/displacement_animation.html)
+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Multiple field animations</font>](https://blendernc.readthedocs.io/en/docs/examples/multiple_field_animations.html)
+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Irregular grid</font>](https://blendernc.readthedocs.io/en/docs/examples/irregular_grid.html)
+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Headless BlenderNC</font>](https://blendernc.readthedocs.io/en/docs/examples/headless_blendernc_simple_animation.html)

## **<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">API Reference</font>**
+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">BlenderNC Add-on API</font>](https://blendernc.readthedocs.io/en/docs/modules/blendernc.html)

## **<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">Help & References</font>**
+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Report</font>](https://blendernc.readthedocs.io/en/docs/help.html)
+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Related Projects</font>](https://blendernc.readthedocs.io/en/docs/help.html#related-projects)
    - [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Underlying Python technologies</font>](https://blendernc.readthedocs.io/en/docs/help.html#underlying-python-technologies)
    - [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Relevant Blender Addons</font>](https://blendernc.readthedocs.io/en/docs/help.html#relevant-blender-addons)
+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Contribute</font>](https://blendernc.readthedocs.io/en/docs/contribute.html)
    - [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Development workflow</font>](https://blendernc.readthedocs.io/en/docs/contribute.html#development-workflow)
    - [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Testing</font>](https://blendernc.readthedocs.io/en/docs/contribute.html#testing)
    - [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Linting</font>](https://blendernc.readthedocs.io/en/docs/contribute.html#linting)
    - [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Distribution</font>](https://blendernc.readthedocs.io/en/docs/contribute.html#distribution)

## <font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">Indices and tables</font>
+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Index</font>](https://blendernc.readthedocs.io/en/docs/genindex.html)
+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Module Index</font>](https://blendernc.readthedocs.io/en/docs/py-modindex.html)
+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Search Page</font>](https://blendernc.readthedocs.io/en/docs/search.html)

## <font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">Support</font>
**<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">BlenderNC</font>**<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);"> </font><font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">is supported by:</font>

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752211903137-18b062c5-0d9b-4bb7-a92e-2daa1c3dda99.png)![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752211912377-0bab80f8-5523-4074-b1c2-445ef5a1eb96.png)

+ **<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">BlenderNC</font>**<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);"> </font><font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">is part of the</font><font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);"> </font>[<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">ECMWF Summer of Weather Code 2021</font>](https://esowc.ecmwf.int/)<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">, an innovation program organised by the</font><font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);"> </font>[<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">European Centre for Medium-Range Weather Forecasts</font>](https://www.ecmwf.int/)<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);"> </font><font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">focusing on weather- and climate-related open-source developments. The sponsored work aims to implement and improve support of weather and climate data visualizations in GRIB format within</font><font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);"> </font>**<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">BlenderNC</font>**<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">.</font>

![](https://cdn.nlark.com/yuque/0/2025/png/44934637/1752211953285-4d813eb4-fd30-4c09-b950-c1fc909d8ee8.png)

+ [<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">Consortium for Ocean-Sea Ice Modelling in Australia</font>](http://cosima.org.au/)<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);"> </font><font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">(COSIMA) funds development of</font><font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);"> </font>**<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">BlenderNC</font>**<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);"> </font><font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">to visualize numerical models of the global ocean and sea ice (</font>[<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">ACCESS-OM2</font>](http://cosima.org.au/index.php/models/access-om2/)<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">).</font>

## <font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">Community</font>
<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">This section show animations submitted by the BlenderNC users.</font>

![](https://cdn.nlark.com/yuque/0/2025/gif/44934637/1752211900131-707fd4be-2980-43bf-9dc6-58c0720f64cf.gif)

<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">The animation by </font>[<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">JoshuaB-L</font>](https://github.com/JoshuaB-L)<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);"> shows equivalent potential temperature (theta-e) of the adiabatic process - air moving across a warming urban surface from 10:00-11:00 am on 16-07-2018 at Potsdamer Platz, Berlin. The wind speed is 7.2 km/h considered a factor of 2 on the Beaufort Scale (‘Light breeze’). The temperature scale is shown in Kelvins (i.e. 20.85 °C - 28.65 °C range). Convection of the rising air parcels is clearly visible from the ground and building surfaces. Heat transfer occurs due to the mixing of warm air (at ground level z0) and cool air (above the building canopy) caused by the turbulent rising eddies. Thus, the ambient air temperature of the urban environment rises. The simulation model used is PALM in LES mode. More information can be found </font>[<font style="color:rgb(41, 128, 185);background-color:rgb(252, 252, 252);">here</font>](https://palm.muk.uni-hannover.de/trac/wiki/doc/tut/palm)<font style="color:rgb(64, 64, 64);background-color:rgb(252, 252, 252);">.</font>

[Welcome to BlenderNC’s documentation! — blendernc 0.4.11 documentation](https://blendernc.readthedocs.io/en/docs/index.html#)

---

