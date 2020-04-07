# 什么是 Booster ？

Booster 是一款专门为移动应用设计的易用、轻量级且可扩展的质量优化框架，其目标主要是为了解决随着 APP 复杂度的提升而带来的性能、稳定性、包体积等一系列质量问题。

Booster 不仅仅只是一个框架，它还提供了性能检测、多线程优化、资源索引内联、资源去冗余、资源压缩、系统 Bug 修复等一系列功能模块，可以使得稳定性能够提升 15% ~ 25%，包体积可以减小 1MB ~ 10MB，甚至更多。

# 为什么是 Booster ？

质量优化是所有应用开发者都要面临的问题，对于 DAU 千万级的 APP 来说，万分之一的崩溃率就意味着上千的用户受到影响，对于长时间使用的 APP 来说，其稳定性关乎着产品的品牌、口碑以及用户的收入，所以更是不容小觑。

随着业务的快速发展，业务复杂度不断提升，我们开始思考：

1. 如何持续保证 APP 的质量？
1. 当 APP 崩溃后，如何快速定位问题所属的业务线？
1. 能不能在上线之前提前发现潜在的质量问题？
1. 能不能对 APP 进行无侵入的全局质量优化而不需要推动各个业务线？

基于这些考虑，Booster 应运而生，经过一年多的时间不断打磨，从线上的数据来看，收益显著。由于目前在质量优化方面基于静态分析的开源项目屈指可数，加上质量优化对于 APP 开发者而言门槛偏高，因此，我们选择了将 Booster 开源，希望更多的开发者和用户能从中受益。

# Booster 的设计思路

可扩展性是 Booster 架构的核心需求，通过功能模块化，让功能开发相对更独立，也方便功能的测试和灰度验证，除此之外，还要解决这些问题：

1. 如何让模块的开发变得更容易？
1. 当功能模块足够多时，如何保证构建的性能？
1. 如何解决开源协议冲突的问题？

为了能很好的解决这些问题，最终 Booster 的架构被设计成如下图所示：

![Booster架构](https://github.com/didi/booster/blob/master/assets/booster-architecture.png?raw=true)

## 如何实现可扩展？

为了实现功能模块的动态发现与加载，Booster 以 SPI (Service Provider Interface) 为基础，通过 *Google AutoService* 简化了 SPI 的配置，在 Booster 中提供了两大类 SPI：

- [Task SPI](https://github.com/didi/booster/blob/master/booster-task-spi)

  *Task SPI* 用于在 Gradle 的 Task Graph 中插入自定义的 task，例如：[booster-task-compression-cwebp](https://github.com/didi/booster/blob/master/booster-task-compression-cwebp), [booster-task-compression-pngquant](https://github.com/didi/booster/blob/master/booster-task-compression-pngquant) 等等。

- [Transformer SPI](https://github.com/didi/booster/blob/master/booster-transform-spi)

  *Transformer SPI* 用于在 *Transform* 的过程中插入自定的 *Transformer* 对字节码进行操作。为了照顾到大多数的开发者，*Booster* 中提供了两种 *Transformer SPI*：

    1. 基于 ASM 的 [ClassTransformer](https://github.com/didi/booster/blob/master/booster-transform-asm/src/main/kotlin/com/didiglobal/booster/transform/asm/ClassTransformer.kt)
    1. 基于 Javassist 的 [ClassTransformer](https://github.com/didi/booster/blob/master/booster-transform-javassist/src/main/kotlin/com/didiglobal/booster/transform/javassist/ClassTransformer.kt)

  开发者可以根据自己的喜好，选择使用 *ASM* 或者 *Javassist*。

## 如何让开发变得更容？

在开发体验和便利性上，*Booster* 主要做了这些事情：

1. 抽象 *Transform* 过程，直接将解析好的 *class* 文件结构暴露给开发者；
1. 将 *Transform* 与 *Gradle* 解耦，在非 *Gradle* 工程中同样可以复用 *Booster* 的 *Transformer*；
1. 通过 [VariantProcessor](https://github.com/didi/booster/blob/master/booster-task-spi/src/main/kotlin/com/didiglobal/booster/task/spi/VariantProcessor.kt) 解决注入外部库的依赖问题，使得大规模字节码注入成为可能；
1. 从 *AGP 3.0* 开始，依次做 *AGP* 做兼容性适配，并抽象出通用的 [Android Gradle API](https://github.com/didi/booster/blob/master/booster-android-gradle-api)，使得开发者不用关心 *AGP* 各版本间的差异；

## 如何保证构建的性能？

1. 一次文件系统 I/O

  从 *Booster* 的源码中可以看到，整个 *Transform* 过程只涉及到一次读写文件系统，所有的 *Transformer* 都是访问内存中的 *Class* 结构

1. 并行 *Transform*

  整个 *Transform* 以文件的粒度进行并行执行，最大限度利用 CPU 资源。

1. 并行写磁盘

  通过并行方式将 *class* 写回 *JAR* 中。

1. 性能测试

  通过 *JMH* 对多个技术方案进行 *benchmark* 测试，选择性能最优的方案，详见：[booster-benchmark](https://github.com/johnsonlee/booster-benchmark)。

## 如何解决开源协议冲突？

在 *Booster* 中，除了 [Task SPI](https://github.com/didi/booster/blob/master/booster-task-spi) 和 [Transform SPI](https://github.com/didi/booster/blob/master/booster-transform-spi) 以外，还提供了一种 SPI —— [Command SPI](https://github.com/didi/booster/blob/master/booster-command/src/main/kotlin/com/didiglobal/booster/command/CommandProvider.kt)。

[Command SPI](https://github.com/didi/booster/blob/master/booster-command/src/main/kotlin/com/didiglobal/booster/command/CommandProvider.kt) 主要是为了解决在 *Apache License* 的协议框下使用采用了 *GPL License* 的开源软件，如：*pngquant* 采用了 *GPL License* 开源许可，直接在项目中使用会有一定的法律风险，所以 *Booster* 的做法是将部分抽象出来，以 *SPI* 的形式在运行时动态发现和加载 *Command SPI* 的实现，这样，既能保证开源许可的合法性，又能使用优秀的 *GPL* 开源软件。
