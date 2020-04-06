# Summary

* [前言](./README.md)

## 字节码简介

* Java 虚拟机
    * [class 文件格式](./jvm/class-file.md)
    * [手写 Class Parser](./jvm/write-class-parser-manually.md)
    * [JVM 指令](./jvm/instructions.md)
    * [栈帧](./jvm/frame.md)
* Dalvik 虚拟机
    * [dex 文件格式](./dalvik/dex-file.md)
    * [Dalvik 指令](./dalvik/instructions.md)

## 操作字节码

* [Java Agent](./instrumentation/java-agent.md)
* [Transform API](./instrumentation/transform-api.md)
* [第一个 Transformer](./instrumentation/first-transformer.md)
* [第一个 VariantProcessor](./instrumentation/first-variant-processor.md)
* [Transformer 搭配 VariantProcessor](./instrumentation/transformer-plus-variant-processor.md)
* [单独使用 Transformer](./instrumentation/standalone-transformer.md)

## 操作资源

* [构建中间产物](./gradle/build-immediates.md)
* [AAPT2](./gradle/aapt2.md)
* [Resource Table](./gradle/resource-table.md)
