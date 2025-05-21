---
title: 天地图 WMTS 能力文档查看
date: 2024-11-12T08:46
tags:
  - 天地图
  - WMTS
---

可通过 https://t0.tianditu.gov.cn/img_w/wmts?request=GetCapabilities
查看对应图层的能力文档

可以看出使用的是 DPI 标准为 96（像素宽度约 0.264mm）

墨卡托投影的瓦片矩阵集

```xml
<TileMatrixSet>
  <ows:Identifier>w</ows:Identifier>
  <ows:SupportedCRS>urn:ogc:def:crs:EPSG::900913</ows:SupportedCRS>
  <TileMatrix>
    <ows:Identifier>1</ows:Identifier>
    <ScaleDenominator>2.958293554545656E8</ScaleDenominator>
    <TopLeftCorner>20037508.3427892 -20037508.3427892</TopLeftCorner>
    <TileWidth>256</TileWidth>
    <TileHeight>256</TileHeight>
    <MatrixWidth>2</MatrixWidth>
    <MatrixHeight>2</MatrixHeight>
  </TileMatrix>
  ...
  <TileMatrix>
	<ows:Identifier>18</ows:Identifier>
	<ScaleDenominator>2256.998866688275</ScaleDenominator>
	<TopLeftCorner>20037508.3427892 -20037508.3427892</TopLeftCorner>
	<TileWidth>256</TileWidth>
	<TileHeight>256</TileHeight>
	<MatrixWidth>262144</MatrixWidth>
	<MatrixHeight>262144</MatrixHeight>
  </TileMatrix>
</TileMatrixSet>
```

经纬度投影（EPSG:4490)的瓦片矩阵集

```xml
<TileMatrixSet>
  <ows:Identifier>c</ows:Identifier>
  <ows:SupportedCRS>urn:ogc:def:crs:EPSG::4490</ows:SupportedCRS>
  <TileMatrix>
    <ows:Identifier>1</ows:Identifier>
    <ScaleDenominator>2.958293554545656E8</ScaleDenominator>
    <TopLeftCorner>90.0 -180.0</TopLeftCorner>
    <TileWidth>256</TileWidth>
    <TileHeight>256</TileHeight>
    <MatrixWidth>2</MatrixWidth>
    <MatrixHeight>1</MatrixHeight>
  </TileMatrix>
  ...
  <TileMatrix>
	<ows:Identifier>18</ows:Identifier>
	<ScaleDenominator>2256.998866688275</ScaleDenominator>
	<TopLeftCorner>90.0 -180.0</TopLeftCorner>
	<TileWidth>256</TileWidth>
	<TileHeight>256</TileHeight>
	<MatrixWidth>262144</MatrixWidth>
	<MatrixHeight>131072</MatrixHeight>
  </TileMatrix>
</TileMatrixSet>
```

天地图同时也提供了 OGC 标准(DPI 90.714) 的瓦片矩阵集
可以在 Arcmap 中正常使用
https://t0.tianditu.gov.cn/img_w/esri/wmts?REQUEST=GetCapabilities&tk=<服务端 tk>

> 在浏览器中预览能力文档时填浏览器端 key，在 arcmap 中使用时使用服务端 key

```xml
<TileMatrixSet>
  <ows:Identifier>w</ows:Identifier>
  <ows:SupportedCRS>urn:ogc:def:crs:EPSG::3857</ows:SupportedCRS>
  <TileMatrix>
	<ows:Identifier>1</ows:Identifier>
	<ScaleDenominator>2.795411320143237E8</ScaleDenominator>
	<TopLeftCorner>-20037508.3427892 20037508.3427892</TopLeftCorner>
	<TileWidth>256</TileWidth>
	<TileHeight>256</TileHeight>
	<MatrixWidth>2</MatrixWidth>
	<MatrixHeight>2</MatrixHeight>
  </TileMatrix>
  ...
  <TileMatrix>
	<ows:Identifier>18</ows:Identifier>
	<ScaleDenominator>2132.7295838495156</ScaleDenominator>
	<TopLeftCorner>-20037508.3427892 20037508.3427892</TopLeftCorner>
	<TileWidth>256</TileWidth>
	<TileHeight>256</TileHeight>
	<MatrixWidth>262144</MatrixWidth>
	<MatrixHeight>262144</MatrixHeight>
  </TileMatrix>
</TileMatrixSet>
```
