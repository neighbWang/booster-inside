# Summary

* [关于本书](./README.md)
* [贡献者](./contributors.md)
* [如何打赏](https://johnsonlee.io/donate/?AliPayQR=/img/AliPayQR.png&WeChatQR=/img/WeChatQR.png)

## 概览

* [Booster 简介](./overview.md)
* [快速上手](./getting-started.md)

## Booster 特性简介

* 性能优化
  * [静态分析](./performance/static-analysis.md)
  * [多线程优化](./performance/multithreading-optimization.md)
  * [SharedPreferences 优化](./performance/shared-preferences-optimization.md)
  * [WebView 预加载](./performance/webview-preloading.md)
* 包体积瘦身
  * WebP 图片压缩
  * PNG 图片压缩
  * ZIP 文件压缩
  * 去冗余资源
  * 资源索引内联
* 系统 bug 修复
  * 系统 bug 兜底
  * Finalizer 导致的 TimeoutException
  * Android 7.0 覆盖安装问题
  * Android 7.1 上 Toast 问题
* 其它
  * 正式包版本检查
  * 权限清单
  * 构建中间产物清单

## Booster 插件开发

* Javassist 还是 ASM？
* 第一个 Transformer
* 第一个 VariantProcessor
* Transformer 与 VariantProcessor 完美组合
* 在 Java 工程中使用 Transformer
* Transformer 实战

## Android 构建概述

* Android Gradle Plugin 概述
* AAPT2 容器
* Resource Table 概述

## Android 构建进阶

* 增量编译概述
* Gradle 缓存概述
* VirtualAPK 插件构建
* Android 构建优化

## 深入字节码

* Java 虚拟机
    * [class 文件格式](./jvm/class-file.md)
    * [JVM 指令](./jvm/instructions.md)
    * 栈帧
    * Java Agent
* Dalvik 虚拟机
    * dex 文件格式
    * Dalvik 指令

