# 手写 Class Parser

可能很多初学者觉得写 *lexer* 和 *parser* 太难了，其实不然，*lexer* 和 *parser* 是编译器中最简单的部分，只要掌握了如何用文法来表达，就基本上能手写 *parser* 了。手写 *parser* 通常采用 *自顶向下* 的解析方式，因为这更容易被人所理解，便于后期的维护。

## *class* 文法

如果用文法表示 *class* 文件结构，则如下所示：

```
<ClassFile>          ::= <MagicNumber>
                         <ClassVersion>
                         <ConstantPool>
                         <ClassMetadata>
                         <Fields>
                         <Methods>
                         <Attributes>

<ClassVersion>       ::= <MinorVersion> <MajorVersion>

<ConstantPool>       ::= <NumberOfConstants> [ <ConstantInfo>, ... ]

<ClassMetadata>      ::= <ClassAccessFlags>
                         <ThisClassIndex>
                         <SuperClassIndex>
                         <NumberOfInterfaces>
                         [ <InterfaceIndex>, ... ]

<Fields>             ::= <NumberOfFields> [ <FieldInfo>, ... ]

<Methods>            ::= <NumberOfMethods> [ <MethodInfo>, ... ]

<Attributes>         ::= <NumberOfAttributes> [ <AttributeInfo> ]

<ConstantInfo>       ::= <ConstantClass>
                       | <ConstantFieldRef>
                       | <ConstantMethodRef>
                       | <ConstantInterfaceMethodRef>
                       | <ConstantString>
                       | <ConstnatInteger>
                       | <ConstantFloat>
                       | <ConstantLong>
                       | <ConstantDouble>
                       | <ConstantNameAndType>
                       | <ConstantUtf8>
                       | <ConstantMethodHandle>
                       | <ConstantMethodType>
                       | <ConstantInvokeDynamic>

<ClassAccessFlags>   ::= ACC_PUBLIC
                       | ACC_PRIVATE
                       | ACC_PROTECTED
                       | ACC_STATIC
                       | ACC_FINAL
                       | ACC_INTERFACE
                       | ACC_ABSTRACT
                       | ACC_SYNTHETIC
                       | ACC_ANNOTATION
                       | ACC_ENUM

<FieldInfo>          ::= <FieldAccessFlags> <NameIndex> <DescriptorIndex> <Attributes>

<MethodInfo>         ::= <MethodAccessFlags> <NameIndex> <DescriptorIndex> <Attributes>

<AttributeInfo>      ::= <ConstantValue>
                       | <Code>
                       | <StackMapTable>
                       | <Exceptions>
                       | <InnerClasses>
                       | <EnclosingMethod>
                       | <Synthetic>
                       | <Signature>
                       | <SourceFile>
                       | <SourceDebugExtension>
                       | <LineNumberTable>
                       | <LocalVariableTable>
                       | <LocalVariableTypeTable>
                       | <Deprecated>
                       | <RuntimeVisibleAnnotations>
                       | <RuntimeInvisibleAnnotations>
                       | <RuntimeVisibleParameterAnnotations>
                       | <RuntimeInvisibleParameterAnnotations>
                       | <RuntimeVisibleTypeAnnotations>
                       | <RuntimeInvisibleTypeAnnotations>
                       | <AnnotationDefault>
                       | <BootstrapMethods>
                       | <MethodParameters>

<FieldAccessFlags>   ::= ACC_PUBLIC
                       | ACC_PRIVATE
                       | ACC_PROTECTED
                       | ACC_STATIC
                       | ACC_FINAL
                       | ACC_VOLATILE
                       | ACC_TRANSIENT
                       | ACC_SYNTHETIC
                       | ACC_ENUM

<MethodAccessFlags>  ::= ACC_PUBLIC
                       | ACC_PRIVATE
                       | ACC_PROTECTED
                       | ACC_STATIC
                       | ACC_FINAL
                       | ACC_SYNCHRONIZED
                       | ACC_BRIDGE
                       | ACC_VARARGS
                       | ACC_NATIVE
                       | ACC_ABSTRACT
                       | ACC_STRICT
                       | ACC_SYNTHETIC

```

按照上面的文法，我们就可以写出一个 *class* 解析器的骨架。

```kotlin:ClassParser.kt
class ClassParser(private val input: DataInputStream, private val needClose: Boolean = false) : Closeable {

    constructor(file: File) : this(file.inputStream(), true)

    constructor(input: InputStream, needClose: Boolean = false) : this(DataInputStream(input), false)

    fun parse(): ClassFile {
        val magic = this.input.readInt().toLong()
        if (magic != 0xcafebabe) {
            throw ParseException("Invalid class file")
        }

        return ClassFile(
                this.input::readInt,
                this::parseConstantPool,
                this::parseMetadata,
                this::parseFields,
                this::parseMethods,
                this::parseAttributes
        )
    }

    private fun parseConstantPool() = parseTypedList(this::parseConstantInfo, input.readUnsignedShort() - 1)

    private fun parseFields() = parseTypedList(this::parseFieldInfo)

    private fun parseMethods() = parseTypedList(this::parseMethodInfo)

    private fun parseAttributes() = parseTypedList(this::parseAttributeInfo)

    private fun parseConstantInfo(): ClassFile.ConstantInfo {
        TODO()
    }

    private fun parseMetadata(): ClassFile.Metadata {
        TODO()
    }

    private fun parseFieldInfo(): ClassFile.FieldInfo {
        TODO()
    }

    private fun parseMethodInfo(): ClassFile.MethodInfo {
        TODO()
    }

    private fun parseAttributeInfo(): ClassFile.AttributeInfo {
        TODO()
    }

    private fun <T> parseTypedList(parse: () -> T, n: Int = input.readUnsignedShort()) = (1..n).map {
        parse()
    }.toList()


    override fun close() {
        if (needClose) {
            this.input.close()
        }
    }

}
```

```kotlin:ClassFile.kt
class ClassParser(private val input: DataInputStream, private val needClose: Boolean = false) : Closeable {

    constructor(file: File) : this(file.inputStream(), true)

    constructor(input: InputStream, needClose: Boolean = false) : this(DataInputStream(input), false)

    fun parse(): ClassFile {
        val magic = this.input.readInt().toLong()
        if (magic != 0xcafebabe) {
            throw ParseException("Invalid classs file")
        }

        return ClassFile(
                this.input::readInt,
                this::parseConstantPool,
                this::parseMetadata,
                this::parseFields,
                this::parseMethods,
                this::parseAttributes
        )
    }

    private fun parseConstantPool() = parseTypedList(this::parseConstantInfo)

    private fun parseFields() = parseTypedList(this::parseFieldInfo)

    private fun parseMethods() = parseTypedList(this::parseMethodInfo)

    private fun parseAttributes() = parseTypedList(this::parseAttributeInfo)

    private fun parseConstantInfo(): ClassFile.ConstantInfo {
        TODO()
    }

    private fun parseMetadata(): ClassFile.Metadata {
        TODO()
    }

    private fun parseFieldInfo(): ClassFile.FieldInfo {
        TODO()
    }

    private fun parseMethodInfo(): ClassFile.MethodInfo {
        TODO()
    }

    private fun parseAttributeInfo(): ClassFile.AttributeInfo {
        TODO()
    }

    private fun <T> parseTypedList(factory: () -> T) = (1..input.readUnsignedShort()).map {
        factory()
    }.toList()


    override fun close() {
        if (needClose) {
            this.input.close()
        }
    }

}
```
