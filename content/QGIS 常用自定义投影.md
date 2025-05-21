---
title: QGIS 常用自定义投影
date: 2024-11-26T09:00
tags:
  - QGIS
aliases:
  - qgis-custom-projection
---

QGIS 在自定义投影方面不如 Arcgis 方便，只能通过 WKT 或者 PROJ 字符串来定义，跟 Arcgis 的 GUI 界面创建投影相比，可以说过于简陋了。甚至自定义投影功能还有一些 BUG（定义投影总是会重复出现两个[^1] 🤣）。

我们可以利用 Arcgis 定义好投影后，导出 `.prj` 文件，将 WKT 字串导入到 QGIS 使用

按此方法，整理了一些适用于 QGIS 常用的投影坐标系。

> [!tip] Tips:
> 下列投影坐标的椭球均为`CGCS2000`。
> 如需`Krassowsky` 请自行替换，参数见文末。

## Albers 正轴等积圆锥投影

适用于**中国全图及南海诸岛作附图**

属于等积投影（Equal-Area Projection），意味着在投影后的地图上，任意区域的面积与实际地球表面上的面积成比例，保持面积不变。

对中国的大陆部分,投影的中央经线常采用`105°E`,标准纬线分别采用`+25°`、`+47°`,在两条标准纬线上没有任何变形。

投影方法:`Albers Equal Area` [**EPSG:9822**]

QGIS Albers China WKT 参数(OGC WKT 2):

```wkt
PROJCRS["Albers China",
    BASEGEOGCRS["China Geodetic Coordinate System 2000",
        DATUM["China 2000",
            ELLIPSOID["CGCS2000",6378137,298.257222101,
                LENGTHUNIT["metre",1]],
            ID["EPSG",1043]],
        PRIMEM["Greenwich",0,
            ANGLEUNIT["Degree",0.0174532925199433]]],
    CONVERSION["unnamed",
        METHOD["Albers Equal Area",
            ID["EPSG",9822]],
        PARAMETER["Latitude of false origin",0,
            ANGLEUNIT["Degree",0.0174532925199433],
            ID["EPSG",8821]],
        PARAMETER["Longitude of false origin",105,
            ANGLEUNIT["Degree",0.0174532925199433],
            ID["EPSG",8822]],
        PARAMETER["Latitude of 1st standard parallel",25,
            ANGLEUNIT["Degree",0.0174532925199433],
            ID["EPSG",8823]],
        PARAMETER["Latitude of 2nd standard parallel",47,
            ANGLEUNIT["Degree",0.0174532925199433],
            ID["EPSG",8824]],
        PARAMETER["Easting at false origin",0,
            LENGTHUNIT["metre",1],
            ID["EPSG",8826]],
        PARAMETER["Northing at false origin",0,
            LENGTHUNIT["metre",1],
            ID["EPSG",8827]]],
    CS[Cartesian,2],
        AXIS["(E)",east,
            ORDER[1],
            LENGTHUNIT["metre",1,
                ID["EPSG",9001]]],
        AXIS["(N)",north,
            ORDER[2],
            LENGTHUNIT["metre",1,
                ID["EPSG",9001]]],
    USAGE[
        SCOPE["Maps"],
        AREA["China"],
        BBOX[0,70,55,140]]]
```

> [!tip] Tips:
>
> - 可设置原点东偏移量(Easting at false origin)值为`5000000`，避免坐标出现负值
> - 添加了使用范围预览框

此投影方式示意图:
![[Albers.jpg]]

> [!note] See Also:
>
> - [阿尔伯斯投影 | Arcmap 帮助文档](https://desktop.arcgis.com/zh-cn/arcmap/latest/map/projections/albers.htm)
> - [EPSG:9822](https://epsg.io/9822-method)
> - [地图投影系列介绍（四）\_ 投影坐标系](https://blog.csdn.net/arcgis_all/article/details/8835832)

> [!warning] 注意:
> 根据`@小雷鸟`的研究，自然资源部标准地图网中标准地图(南海诸岛作附图)的原始投影定义应当是 Albers 投影，中央经线为 109.5°[^2]

## Lambert 正轴等角圆锥投影

等角圆锥投影保持局部角度不变，即地图上的小区域形状与实际地理形状相似，适用于中纬度地区。

投影方法: `Lambert Conic Conformal (2SP)` [EPSG:9802]

> [!note] See Also:
>
> - [兰勃特等角圆锥投影 | Arcmap 帮助文档](https://desktop.arcgis.com/zh-cn/arcmap/latest/map/projections/lambert-conformal-conic.htm)
> - [EPSG:9802](https://epsg.io/9802-method)

QGIS Lambert China WKT 参数(OGC WKT 2):

```wkt
PROJCRS["Lambert China",
    BASEGEOGCRS["China Geodetic Coordinate System 2000",
        DATUM["China 2000",
            ELLIPSOID["CGCS2000",6378137,298.257222101,
                LENGTHUNIT["metre",1]],
            ID["EPSG",1043]],
        PRIMEM["Greenwich",0,
            ANGLEUNIT["Degree",0.0174532925199433]]],
    CONVERSION["unnamed",
        METHOD["Lambert Conic Conformal (2SP)",
            ID["EPSG",9802]],
        PARAMETER["Easting at false origin",0,
            LENGTHUNIT["metre",1],
            ID["EPSG",8826]],
        PARAMETER["Northing at false origin",0,
            LENGTHUNIT["metre",1],
            ID["EPSG",8827]],
        PARAMETER["Longitude of false origin",105,
            ANGLEUNIT["Degree",0.0174532925199433],
            ID["EPSG",8822]],
        PARAMETER["Latitude of 1st standard parallel",25,
            ANGLEUNIT["Degree",0.0174532925199433],
            ID["EPSG",8823]],
        PARAMETER["Latitude of 2nd standard parallel",47,
            ANGLEUNIT["Degree",0.0174532925199433],
            ID["EPSG",8824]],
        PARAMETER["Latitude of false origin",0,
            ANGLEUNIT["Degree",0.0174532925199433],
            ID["EPSG",8821]]],
    CS[Cartesian,2],
        AXIS["(E)",east,
            ORDER[1],
            LENGTHUNIT["metre",1,
                ID["EPSG",9001]]],
        AXIS["(N)",north,
            ORDER[2],
            LENGTHUNIT["metre",1,
                ID["EPSG",9001]]],
    USAGE[
        SCOPE["Maps"],
        AREA["China"],
        BBOX[0,70,55,140]]]
```

此投影方式示意图:
![[Lambert.jpg]]

## Azimuthal equidistant 等距方位投影

等距方位投影可以保留距中心点的距离和方向。

投影方法: `Azimuthal Equidistant` [EPSG:1125]

> 一般竖版中国地图会采用此投影，中央经线为 105°，起始纬线为 35°。

Azimuthal equidistant WKT 参数(OGC WKT 2):

```wkt
PROJCRS["China Azimuthal equidistant",
    BASEGEOGCRS["China Geodetic Coordinate System 2000",
        DATUM["China 2000",
            ELLIPSOID["CGCS2000",6378137,298.257222101,
                LENGTHUNIT["metre",1]],
            ID["EPSG",1043]],
        PRIMEM["Greenwich",0,
            ANGLEUNIT["Degree",0.0174532925199433]]],
    CONVERSION["unnamed",
        METHOD["Azimuthal Equidistant",
            ID["EPSG",1125]],
        PARAMETER["Latitude of natural origin",35,
            ANGLEUNIT["Degree",0.0174532925199433],
            ID["EPSG",8801]],
        PARAMETER["Longitude of natural origin",105,
            ANGLEUNIT["Degree",0.0174532925199433],
            ID["EPSG",8802]],
        PARAMETER["False easting",0,
            LENGTHUNIT["metre",1],
            ID["EPSG",8806]],
        PARAMETER["False northing",0,
            LENGTHUNIT["metre",1],
            ID["EPSG",8807]]],
    CS[Cartesian,2],
        AXIS["(E)",east,
            ORDER[1],
            LENGTHUNIT["metre",1,
                ID["EPSG",9001]]],
        AXIS["(N)",north,
            ORDER[2],
            LENGTHUNIT["metre",1,
                ID["EPSG",9001]]]]
```

此投影方式示意图:
![[Azimuthal.jpg]]

> [!note] See Also:
>
> - [等距方位 (Azimuthal equidistant) 投影 | Arcmap 帮助文档](https://desktop.arcgis.com/zh-cn/arcmap/latest/map/projections/azimuthal-equidistant.htm)

## Vertical Perspective 垂直近侧透视投影

此地图投影效果大致如同从卫星进行观察，能得到模拟地球形状的地图。

QGIS 中已包含此投影（EPSG:54049)，但默认经度和纬度都是 0，所以投影后的地图正对非洲地区。

若以中国为研究区可设置中央经线为 105°，纬度为 0°（此时中国在偏上方）。

效果如图：

![[垂直近侧透视example.jpg]]

Vertical Perspective WKT 参数(OGC WKT 2)

```wkt
PROJCRS["World_Vertical_Perspective",
    BASEGEOGCRS["WGS 84",
        DATUM["World Geodetic System 1984",
            ELLIPSOID["WGS 84",6378137,298.257223563,
                LENGTHUNIT["metre",1]]],
        PRIMEM["Greenwich",0,
            ANGLEUNIT["Degree",0.0174532925199433]]],
    CONVERSION["World_Vertical_Perspective",
        METHOD["Vertical Perspective",
            ID["EPSG",9838]],
        PARAMETER["Latitude of topocentric origin",0,
            ANGLEUNIT["Degree",0.0174532925199433],
            ID["EPSG",8834]],
        PARAMETER["Longitude of topocentric origin",105,
            ANGLEUNIT["Degree",0.0174532925199433],
            ID["EPSG",8835]],
        PARAMETER["Viewpoint height",35800000,
            LENGTHUNIT["metre",1],
            ID["EPSG",8840]]],
    CS[Cartesian,2],
        AXIS["(E)",east,
            ORDER[1],
            LENGTHUNIT["metre",1]],
        AXIS["(N)",north,
            ORDER[2],
            LENGTHUNIT["metre",1]],
    USAGE[
        SCOPE["Not known."],
        AREA["World."],
        BBOX[-90,-180,90,180]]]
```

> [!note] See Also:
> 调整远近及添加大气效果，参考 GIS 荟的这篇文章: [ArcGIS 实现球状地图 Amazing！](https://mp.weixin.qq.com/s/1FxdP2TATooVPshqy6_Qlg)

`Krassowsky`椭球参数

```
BASEGEOGCRS["unknown",
    DATUM["Unknown based on Krassovsky, 1942 ellipsoid",
        ELLIPSOID["Krassovsky, 1942",6378245,298.3,
            LENGTHUNIT["metre",1,
                ID["EPSG",9001]]]],
    PRIMEM["Greenwich",0,
        ANGLEUNIT["degree",0.0174532925199433],
        ID["EPSG",8901]]],
```

[^1]: https://github.com/qgis/QGIS/issues/57239
[^2]: 小雷鸟的窝, 小雷鸟. 标准地图，想说爱你不容易 关于标准地图投影方式的判定。[EB/OL]. (2022-04-10)[2024-11-27]. https://mp.weixin.qq.com/s/GW6Vs0dnkxb7QE0yrM-xqg.
