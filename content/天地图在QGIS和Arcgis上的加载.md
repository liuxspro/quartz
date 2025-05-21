---
title: 天地图在 QGIS 和 Arcgis 上的加载
date: 2024-11-12T16:54:00
tags:
  - QGIS
  - Arcgis
  - GIS
  - 天地图
---

## 准备工作

### Token 申请

- 登录 国家地理信息公共服务平台（天地图）
- 选择 开发平台 > 控制台 > 创建应用

### 我该选择什么类型的 Token ？

目前，天地图有三种类型的 Token，分别为浏览器端、服务端、Android 平台

tk 类型是严格区分的，比如在浏览器中访问使用服务端的资源时，就会提示权限类型错误：

```json
{"msg":"权限类型错误","resolve":"Key权限类型为:服务端，请使用服务端访问！","code":12}
```

天地图是根据`User-Agent`来区分浏览器和服务端的，`User-Agent`中含有"Mozilla"会被识别为浏览器端

比如，Arcgis 请求时的`User-Agent`为`ArcGIS Client Using WinInet`，所以应使用**服务端**；
QGIS 请求时的`User-Agent`为 `Mozilla/5.0 QGIS/34000/Windows 11 Version 2009` 应使用浏览器端。

> QGIS 可在设置中设置用户代理前缀（默认为 `Mozilla/5.0`），如修改为其他前缀，则应使用服务器端 tk。
> 不推荐修改此设置，可能会引起其他地图源的加载出现异常。

目前，Android 平台的 tk 均可在浏览器或服务器端使用，如果不清楚选择什么类型的，可尝试使用 Android 平台。

## QGIS 加载天地图

### 通过 XYZ 瓦片链接添加

这也是[官网示例](http://lbs.tianditu.gov.cn/server/MapService.html)的方式

XYZ URL 链接格式如下:

```text
http://t0.tianditu.gov.cn/img_w/wmts?SERVICE=WMTS&REQUEST=GetTile&VERSION=1.0.0&LAYER=img&STYLE=default&TILEMATRIXSET=w&FORMAT=tiles&TILEMATRIX={z}&TILEROW={y}&TILECOL={x}&tk=您的密钥
```

其中：
LAYER=img_w 为选择图层
TILEMATRIXSET=w 为选择投影（w: 墨卡托投影，c:经纬度投影）

各图层名称如下（墨卡托投影）：

| name  | 图层名称 |
| ----- | -------- |
| vec_w | 矢量底图 |
| cva_w | 矢量注记 |
| img_w | 影像底图 |
| cia_w | 影像注记 |
| ter_w | 地形晕染 |
| cta_w | 地形注记 |
| ibo_w | 全球境界 |

> 如果添加 XYZ 后仍无法访问，尝试设置**来源**(Referer)为`https://www.tianditu.gov.cn/`

![[Pasted image 20241111161902.png]]

### 通过 Tianditu Tools 插件加载

如果觉得这样添加七个图层太过繁琐，且容易出错，QGIS 插件库内有 [TianDiTu Tools](https://plugins.qgis.org/plugins/tianditu-tools/) 插件可以使用。

## Arcmap 加载天地图

Arcmap 可通过 WMTS 服务器添加天地图
以添加**影像底图**（img_w)为例
WMTS 服务器地址:

```text
http://t0.tianditu.gov.cn/img_w/esri/wmts
```

需添加自定义参数 tk
![[Pasted image 20241118164502.png]]

> [!warning] 注意:
>
> - 这里 URL 中有`/ersi`，这是符合 OGC 标准的 WMTS 服务，去掉 esri 是国标 DPI 96 标准的。
> - DPI 96 在 QGIS 或 Arcmap 中加载会有偏移。

## Arcgis Pro 加载天地图

Arcgis Pro 加载天地图的方式与 Arcmap 相似，均是通过 WMTS 服务器并设置自定义参数来添加。

在`插入`选项卡中，点击`连接`>`服务器`>`新建 WMTS 服务器`，输入 URL 以及自定义请求参数即可。

![[GISPRO.jpg]]

> [!note] See Also:
> [[天地图WMTS能力文档查看]]
