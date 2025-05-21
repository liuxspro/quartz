---
title: QGIS通过 WMTS 方式加载天地图
date: 2024-11-12T10:56
tags:
  - QGIS
---

先说结论，可以加载，但有很大偏移。

天地图 WMTS 服务是使用的 96 DPI 标准，QGIS 使用 OGC 标准（90.714 DPI，标准像素宽度定义为 0.28mm），所以有很大偏移。

WMTS 服务地址: 
```
https://t0.tianditu.gov.cn/img_c/wmts?request=GetCapabilities&service=wmts&tk=<tk>
```
同时勾选`忽略功能描述中报告的GetMap/GetTile/GetLegendGraphicURI地址`才能让QGIS请求的瓦片携带tk。

> [!note] See Also:
> - [[QGIS源码中WMS定义的像素大小]]
> - [Tianditu cannot be loaded in QGis WMS/WMTS · Issue #58579 · qgis/QGIS](https://github.com/qgis/QGIS/issues/58579)

