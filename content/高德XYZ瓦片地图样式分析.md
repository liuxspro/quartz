---
title: 高德 XYZ 瓦片地图样式分析
date: 2025-03-30T20:59
tags:
  - 高德地图
  - GIS
---

url 来源可参考高德地图添加 XYZ 栅格图层中的示例（https://lbs.amap.com/demo/javascript-api/example/thirdlayer/custom-grid-map）

```
https://wprd0{1,2,3,4}.is.autonavi.com/appmaptile?x=[x]&y=[y]&z=[z]&size=1&scl=1&style=8&ltype=11'
```

QGIS 适用的 XYZ 格式:

```
https://webst04.is.autonavi.com/appmaptile?lang=zh_cn&scl=1&style=10&x={x}&y={y}&z={z}
```

> 域名`webst`或者`wprd`均可

url 中主要有 style、lang、scl、ltype 几个参数，可控制瓦片地图样式。在 XiaohuanJiang [^1]分析的基础上，自己又做了一些研究。

## 参数
### style

`style` 控制地图样式，6 为卫星影像，7~10 均为矢量

以瓦片`x=1691 y=816 z=11`，各个 style 瓦片如下:

> `https://webst04.is.autonavi.com/appmaptile?lang=zh_cn&scl=1&style=6&x=1691&y=816&z=11`

| Style |                  瓦片                  |               说明               |
| :---: | :----------------------------------: | :----------------------------: |
|   6   | ![[Pasted image 20250330203843.png]] |              卫星影像              |
|   7   | ![[Pasted image 20250330203820.png]] |          矢量地图<br>字体较大          |
|   8   | ![[Pasted image 20250330204000.png]] |       仅注记<br>字体比较小<br>透明       |
|   9   | ![[Pasted image 20250330204043.png]] | 矢量地图<br>字体较大<br>与 7 相同，但是没有图标  |
|  10   | ![[Pasted image 20250330204141.png]] | 矢量地图<br>字体较大<br>与 9 相同，但是标注了路名 |

### scl

`scl`控制瓦片大小，`scl=1`为 256px 的瓦片；`scl=2`为 512px 的瓦片，但是对卫星影像(style=6)无效，矢量地图均无注记。
![[Pasted image 20250517231342.png]]

### lang

`lang`控制显示语言，`lang=zh_cn` 中文注记，`lang=en` 英文注记

![[Pasted image 20250517231535.png]]

### ltype

`ltype`是控制是否显示地图要素的，可控制的要素有自然要素（包括水体、绿地、建筑等）、路网、注记，经过测试，发现是基于位掩码（Bitmask）来控制的，如下表所示。

| 位置 |   0    |      0       |      0       |        0         |
| :--: | :----: | :----------: | :----------: | :--------------: |
| 含义 | 无意义 | 是否显示注记 | 是否显示路网 | 是否显示自然要素 |

```
1（二进制 0b0001）表示显示自然要素
2（二进制 0b0010）表示显示路网
4（二进制 0b0100）表示显示注记
```

比如要显示路网+注记，ltype 值就是 2+4=6

## 参考资料:

[^1]: 高德 WMTS 瓦片地图服务地图图源规律[EB/OL]. (2019-03-27). https://www.jianshu.com/p/e34f85029fd7.
