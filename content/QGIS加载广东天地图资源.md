---
title: QGIS 加载广东天地图资源
date: 2024-12-11T11:45
tags:
  - QGIS
  - 天地图
---

来自[广东天地图-资源中心](https://guangdong.tianditu.gov.cn/GeoResourceCenter/index.html#/mall)(无条件共享)

以[广东省永久基本农田保护图斑](https://guangdong.tianditu.gov.cn/GeoResourceCenter/index.html#/mall/detail?id=67&type=0)为例
其服务 URL 为：

```
https://guangdong.tianditu.gov.cn/server/GDJBNTBHTB/
```

WMS 服务地址为：

```
https://guangdong.tianditu.gov.cn/server/GDJBNTBHTB/wms?SERVICE=WMS&VERSION=1.1.1&REQUEST=GetCapabilities
```

WMTS 服务地址：

```
https://guangdong.tianditu.gov.cn/server/GDJBNTBHTB/wmts?SERVICE=WMTS&VERSION=1.0.0&REQUEST=GetCapabilities
```

### WMS 方式加载

QGIS 可通过 WMS 方式加载，这种方式没有偏移，图像质量佳（图 1），但缺点是绘制速度略慢，超过最大层级（15级）后不会显示（图 2）。

### WMTS 方式加载

虽然提供了 3 个瓦片矩阵集，但均不是 OGC 标准(default028mm)，通过 WMTS 方式加载有一定的偏移，因此需要做一点改动。

从 WMTS 服务地址，很容易拿到瓦片的 URL 地址：

```
https://guangdong.tianditu.gov.cn/server/GDJBNTBHTB/wmts?SERVICE=WMTS&REQUEST=GetTile&VERSION=1.0.0&LAYER=GDJBNTBHTB&STYLE=GDJBNTBHTB&FORMAT=image%2Ftile&TILEMATRIXSET=GDJBNTBHTB_Matrix_1&TILEMATRIX=8&TILEROW=49&TILECOL=206
```

将其填入标准 4326 瓦片 WMTS 服务中即可。

也可以使用 Tile 接口的瓦片 URL 地址，更加简短:

```
https://guangdong.tianditu.gov.cn/server/GDJBNTBHTB/DataServer?l={z}&x={x}&y={y}
```

![[Pasted image 20241211170217.png]]
图 1:对比 WMTS 和 WMS，WMS 图片质量更佳（图斑缝隙较明显）
![[Pasted image 20241211170411.png]]
图 2: z>15 级时 WMS 服务不显示，WMTS 显示的是 z=15 级的放大版
