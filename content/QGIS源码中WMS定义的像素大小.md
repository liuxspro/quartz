---
title: QGIS 源码中 WMS 定义的像素大小
date: 2024-11-12T10:36
tags:
  - QGIS
---

QGIS源码中WMS定义的像素大小
https://github.com/qgis/QGIS/blob/2897024aca21bbcc91a31f8487da4270e40db2e3/src/providers/wms/qgswmscapabilities.cpp#L1861
```cpp
// the magic number below is "standardized rendering pixel size" defined
// in WMTS (and WMS 1.3) standard, being 0.28 pixel
tileMatrix.tres = tileMatrix.scaleDenom * 0.00028 / metersPerUnit;
```

> [!note] See Also:
> [修改QGIS来支持DPI为96的WMTS/WMS服务 - 乌合之众 - 博客园](https://www.cnblogs.com/oloroso/p/9553207.html)

