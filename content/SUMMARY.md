# Summary

* [关于本书](./README.md)
* [贡献者](./contributors.md)
* [买杯咖啡](./donate.md)

## 概览

* [Booster 简介](./overview.md)
* [快速上手](./getting-started.md)

## Booster 特性简介

* 性能优化
  * [静态分析](./feature/performance/static-analysis.md)
  * [多线程优化](./feature/performance/multithreading-optimization.md)
  * [SharedPreferences 优化](./feature/performance/shared-preferences-optimization.md)
  * [WebView 预加载](./feature/performance/webview-preloading.md)
* 包体积瘦身
  * [PNG 图片压缩](./feature/shrink/png-compression.md)
  * [WebP 图片压缩](./feature/shrink/webp-compression.md)
  * [ZIP 文件压缩](./feature/shrink/zip-compression.md)
  * [移除冗余资源](./feature/shrink/res-deredundancy.md)
  * [资源索引内联](./feature/shrink/res-index-inline.md)
* 系统 bug 修复
  * [为系统崩溃兜底](./feature/bugfix/prevent-crash-from-system-bug.md)
  * [Finalizer 导致的 TimeoutException](./feature/bugfix/finalizer-timeout-exception.md)
  * [资源为 null 的问题](./feature/bugfix/null-resource-assets.md)
  * [Android 7.1 Toast 崩溃](./feature/bugfix/toast-crash-on-android-25.md)
* 其它
  * [Release 构建依赖检查](./feature/misc/dependencies-check-on-release-build.md)
  * [Android 权限清单](./feature/misc/android-permission-list.md)
  * [动态库清单](./feature/misc/shared-library-list.md)
  * [构建中间产物清单](./feature/misc/build-artifact-list.md)

## Booster 插件开发

* [Javassist 还是 ASM？](./developer/javassist-or-asm.md)
* [第一个 Transformer](./developer/first-class-transformer.md)
* [第一个 VariantProcessor](./developer/first-variant-processor.md)
* [Transformer + VariantProcessor](./developer/class-transformer-plus-variant-processor.md)
* [在 *Task* 中使用 *Transformer*](./developer/using-transformer-in-task.md)
* [脱离 Gradle 环境](./developer/standalone-transformer.md)
* [FAQ](./developer/faq.md)

## Android 构建概述

* [Android Gradle Plugin 概述](./agp/apk-build-process.md)
* [AAPT2 容器](./agp/aapt2.md)
* [Resource Table 概述](./agp/resources-arsc.md)

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

