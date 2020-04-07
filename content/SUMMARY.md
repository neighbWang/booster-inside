# Summary

* [前言](./README.md)

## 字节码简介

* Java 虚拟机
    * [class 文件格式](./jvm/class-file.md)
    * [手写 Class Parser](./jvm/write-class-parser-manually.md)
    * [JVM 指令](./jvm/instructions.md)
    * [栈帧](./jvm/frame.md)
    * [Java Agent](./jvm/java-agent.md)
* Dalvik 虚拟机
    * [dex 文件格式](./dalvik/dex-file.md)
    * [Dalvik 指令](./dalvik/instructions.md)

## Android 应用构建

* [Android Gradle Plugin 概述](./agp/overview.md)
* [Transform API 概述](./agp/transform-api.md)
* [AAPT2 容器](./agp/aapt2.md)
* [Resource Table 概述](./agp/resource-table.md)
* [VirtualAPK 插件构建方案](./agp/virtual-apk.md)
* [构建面临的挑战](./agp/challenge.md)
* [构建优化](./agp/build-optimziation.md)

## 基于 Booster 开发插件

* [第一个 Transformer](./booster/first-transformer.md)
* [第一个 VariantProcessor](./booster/first-variant-processor.md)
* [Transformer 搭配 VariantProcessor](./booster/transformer-plus-variant-processor.md)
* [单独使用 Transformer](./booster/standalone-transformer.md)

## 基于 Gradle API 开发插件

* Gradle 版本差异
