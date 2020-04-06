# JVM 指令

在 JVM 规范中定义了将近 200+ 个指令，如下表所示：

|  op  | 语法                            | 栈                                       | 描述                                                                              |
|:----:|---------------------------------|------------------------------------------|-----------------------------------------------------------------------------------|
| 0x00 |*nop*                            |无变化                                    | 不执行任何操作                                                                    |
| 0x01 |*aconst_null*                    |*... → ...,null*                          | 将 *null* 引用压入栈[^1]顶                                                        |
| 0x02 |*iconst_m1*                      |*... → ...,-1*                            | 将 *int* 常量值 *-1* 压入栈顶                                                     |
| 0x03 |*iconst_0*                       |*... → ...,0*                             | 将 *int* 常量值 *0* 压入栈顶                                                      |
| 0x04 |*iconst_1*                       |*... → ...,1*                             | 将 *int* 常量值 *1* 压入栈顶                                                      |
| 0x05 |*iconst_2*                       |*... → ...,2*                             | 将 *int* 常量值 *2* 压入栈顶                                                      |
| 0x06 |*iconst_3*                       |*... → ...,3*                             | 将 *int* 常量值 *3* 压入栈顶                                                      |
| 0x07 |*iconst_4*                       |*... → ...,4*                             | 将 *int* 常量值 *4* 压入栈顶                                                      |
| 0x08 |*iconst_5*                       |*... → ...,5*                             | 将 *int* 常量值 *5* 压入栈顶                                                      |
| 0x09 |*lconst_0*                       |*... → ...,0L*                            | 将 *long* 常量值 *0L* 压入栈顶                                                    |
| 0x0a |*lconst_1*                       |*... → ...,1L*                            | 将 *long* 常量值 *1L* 压入栈顶                                                    |
| 0x0b |*fconst_0*                       |*... → ...,0.0f*                          | 将 *float* 常量值 *0.0f* 压入栈顶                                                 |
| 0x0c |*fconst_1*                       |*... → ...,1.0f*                          | 将 *float* 常量值 *1.0f* 压入栈顶                                                 |
| 0x0d |*fconst_2*                       |*... → ...,2.0f*                          | 将 *float* 常量值 *1.0f* 压入栈顶                                                 |
| 0x0e |*dconst_0*                       |*... → ...,0.0*                           | 将 *double* 常量值 *0.0* 压入栈顶                                                 |
| 0x0f |*dconst_1*                       |*... → ...,1.0*                           | 将 *double* 常量值 *1.0* 压入栈顶                                                 |
| 0x10 |*bipush,AA[^2]*                  |*... → ...,v*                             | 将立即数[^3] *AA* 压入栈顶                                                        |
| 0x11 |*sipush,AAAA[^4]*                |*... → ...,v*                             | 将立即数 *AAAA* 压入栈顶                                                          |
| 0x12 |*ldc,AA*                         |*... → ...,v*                             | 将常量池中索引为 *AA* 的常量压入栈顶                                              |
| 0x13 |*ldc_w,AAAA*                     |*... → ...,v*                             | 将常量池中索引为 *AAAA* 的常量压入栈顶                                            |
| 0x14 |*ldc2_w,AAAA*                    |*... → ...,v*                             | 将常量池中索引为 *AAAA* 的 *long* 或 *double* 常量压入栈顶                        |
| 0x15 |*iload,AA*                       |*... → ...,v*                             | 将本地变量表中索引为 *AA* 的 *int* 变量压入栈顶                                   |
| 0x16 |*lload,AA*                       |*... → ...,v*                             | 将本地变量表中索引为 *AA* 的 *long* 变量压入栈顶                                  |
| 0x17 |*fload,AA*                       |*... → ...,v*                             | 将本地变量表中索引为 *AA* 的 *float* 变量压入栈顶                                 |
| 0x18 |*dload,AA*                       |*... → ...,v*                             | 将本地变量表中索引为 *AA* 的 *double* 变量压入栈顶                                |
| 0x19 |*aload,AA*                       |*... → ...,v*                             | 将本地变量表中索引为 *AA* 的 *aref* 压入栈顶                                      |
| 0x1a |*iload_0*                        |*... → ...,0*                             | 将本地变量表中索引为 *0* 的 *int* 变量压入栈顶                                    |
| 0x1b |*iload_1*                        |*... → ...,1*                             | 将本地变量表中索引为 *1* 的 *int* 变量压入栈顶                                    |
| 0x1c |*iload_2*                        |*... → ...,2*                             | 将本地变量表中索引为 *2* 的 *int* 变量压入栈顶                                    |
| 0x1d |*iload_3*                        |*... → ...,3*                             | 将本地变量表中索引为 *3* 的 *int* 变量压入栈顶                                    |
| 0x1e |*lload_0*                        |*... → ...,0L*                            | 将本地变量表中索引为 *0* 的 *long* 变量压入栈顶                                   |
| 0x1f |*lload_1*                        |*... → ...,1L*                            | 将本地变量表中索引为 *1* 的 *long* 变量压入栈顶                                   |
| 0x20 |*lload_2*                        |*... → ...,2L*                            | 将本地变量表中索引为 *2* 的 *long* 变量压入栈顶                                   |
| 0x21 |*lload_3*                        |*... → ...,3L*                            | 将本地变量表中索引为 *3* 的 *long* 变量压入栈顶                                   |
| 0x22 |*fload_0*                        |*... → ...,0.0f*                          | 将本地变量表中索引为 *0* 的 *float* 变量压入栈顶                                  |
| 0x23 |*fload_1*                        |*... → ...,1.0f*                          | 将本地变量表中索引为 *1* 的 *float* 变量压入栈顶                                  |
| 0x24 |*fload_2*                        |*... → ...,2.0f*                          | 将本地变量表中索引为 *2* 的 *float* 变量压入栈顶                                  |
| 0x25 |*fload_3*                        |*... → ...,3.0f*                          | 将本地变量表中索引为 *3* 的 *float* 变量压入栈顶                                  |
| 0x26 |*dload_0*                        |*... → ...,0.0*                           | 将本地变量表中索引为 *0* 的 *double* 变量压入栈顶                                 |
| 0x27 |*dload_1*                        |*... → ...,1.0*                           | 将本地变量表中索引为 *1* 的 *double* 变量压入栈顶                                 |
| 0x28 |*dload_2*                        |*... → ...,2.0*                           | 将本地变量表中索引为 *2* 的 *double* 变量压入栈顶                                 |
| 0x29 |*dload_3*                        |*... → ...,3.0*                           | 将本地变量表中索引为 *3* 的 *double* 变量压入栈顶                                 |
| 0x2a |*aload_0*                        |*... → ...,aref*                          | 将本地变量表中索引为 *0* 的 *aref* 压入栈顶                                       |
| 0x2b |*aload_1*                        |*... → ...,aref*                          | 将本地变量表中索引为 *1* 的 *aref* 压入栈顶                                       |
| 0x2c |*aload_2*                        |*... → ...,aref*                          | 将本地变量表中索引为 *2* 的 *aref* 压入栈顶                                       |
| 0x2d |*aload_3*                        |*... → ...,aref*                          | 将本地变量表中索引为 *3* 的 *aref* 压入栈顶                                       |
| 0x2e |*iaload*                         |*...,aaref,index → ...,v*                 | 将数组 *aaref* 中索引为 *index (int)* 的 *int* 值压入栈顶                         |
| 0x2f |*laload*                         |*...,aaref,index → ...,v*                 | 将数组 *aaref* 中索引为 *index (int)* 的 *long* 值压入栈顶                        |
| 0x30 |*faload*                         |*...,aaref,index → ...,v*                 | 将数组 *aaref* 中索引为 *index (int)* 的 *float* 值压入栈顶                       |
| 0x31 |*daload*                         |*...,aaref,index → ...,v*                 | 将数组 *aaref* 中索引为 *index (int)* 的 *double* 值压入栈顶                      |
| 0x32 |*aaload*                         |*...,aaref,index → ...,v*                 | 将数组 *aaref* 中索引为 *index (int)* 的 *reference* 值压入栈顶                   |
| 0x33 |*baload*                         |*...,aaref,index → ...,v*                 | 将数组 *aaref* 中索引为 *index (int)* 的 *byte* 或 *boolean* 值压入栈顶           |
| 0x34 |*caload*                         |*...,aaref,index → ...,v*                 | 将数组 *aaref* 中索引为 *index (int)* 的 *char* 值压入栈顶                        |
| 0x35 |*saload*                         |*...,aaref,index → ...,v*                 | 将数组 *aaref* 中索引为 *index (int)* 的 *short* 值压入栈顶                       |
| 0x36 |*istore,AA*                      |*...,v → ...,*                            | 将 *int* 值从栈顶弹出，并赋值给本地变量表中索引为 *AA* 的本地变量                 |
| 0x37 |*lstore,AA*                      |*...,v → ...,*                            | 将 *long* 值从栈顶弹出，并赋值给本地变量表中索引为 *AA* 的本地变量                |
| 0x38 |*fstore,AA*                      |*...,v → ...,*                            | 将 *float* 值从栈顶弹出，并赋值给本地变量表中索引为 *AA* 的本地变量               |
| 0x39 |*dstore,AA*                      |*...,v → ...,*                            | 将 *double* 值从栈顶弹出，并赋值给本地变量表中索引为 *AA* 的本地变量              |
| 0x3a |*astore,AA*                      |*...,v → ...,*                            | 将 *reference* 值从栈顶弹出，并赋值给本地变量表中索引为 *AA* 的本地变量           |
| 0x3b |*istore_0*                       |*...,v → ...,*                            | 将 *int* 值从栈顶弹出，并赋值给本地变量表中索引为 *0* 的本地变量                  |
| 0x3c |*istore_1*                       |*...,v → ...,*                            | 将 *int* 值从栈顶弹出，并赋值给本地变量表中索引为 *1* 的本地变量                  |
| 0x3d |*istore_2*                       |*...,v → ...,*                            | 将 *int* 值从栈顶弹出，并赋值给本地变量表中索引为 *2* 的本地变量                  |
| 0x3e |*istore_3*                       |*...,v → ...,*                            | 将 *int* 值从栈顶弹出，并赋值给本地变量表中索引为 *3* 的本地变量                  |
| 0x3f |*lstore_0*                       |*...,v → ...,*                            | 将 *long* 值从栈顶弹出，并赋值给本地变量表中索引为 *0* 的本地变量                 |
| 0x40 |*lstore_1*                       |*...,v → ...,*                            | 将 *long* 值从栈顶弹出，并赋值给本地变量表中索引为 *1* 的本地变量                 |
| 0x41 |*lstore_2*                       |*...,v → ...,*                            | 将 *long* 值从栈顶弹出，并赋值给本地变量表中索引为 *2* 的本地变量                 |
| 0x42 |*lstore_3*                       |*...,v → ...,*                            | 将 *long* 值从栈顶弹出，并赋值给本地变量表中索引为 *3* 的本地变量                 |
| 0x43 |*fstore_0*                       |*...,v → ...,*                            | 将 *float* 值从栈顶弹出，并赋值给本地变量表中索引为 *0* 的本地变量                |
| 0x44 |*fstore_1*                       |*...,v → ...,*                            | 将 *float* 值从栈顶弹出，并赋值给本地变量表中索引为 *1* 的本地变量                |
| 0x45 |*fstore_2*                       |*...,v → ...,*                            | 将 *float* 值从栈顶弹出，并赋值给本地变量表中索引为 *2* 的本地变量                |
| 0x46 |*fstore_3*                       |*...,v → ...,*                            | 将 *float* 值从栈顶弹出，并赋值给本地变量表中索引为 *3* 的本地变量                |
| 0x47 |*dstore_0*                       |*...,v → ...,*                            | 将 *double* 值从栈顶弹出，并赋值给本地变量表中索引为 *0* 的本地变量               |
| 0x48 |*dstore_1*                       |*...,v → ...,*                            | 将 *double* 值从栈顶弹出，并赋值给本地变量表中索引为 *1* 的本地变量               |
| 0x49 |*dstore_2*                       |*...,v → ...,*                            | 将 *double* 值从栈顶弹出，并赋值给本地变量表中索引为 *2* 的本地变量               |
| 0x4a |*dstore_3*                       |*...,v → ...,*                            | 将 *double* 值从栈顶弹出，并赋值给本地变量表中索引为 *3* 的本地变量               |
| 0x4b |*astore_0*                       |*...,aref → ...,*                         | 将 *reference* 值从栈顶弹出，并赋值给本地变量表中索引为 *0* 的本地变量            |
| 0x4c |*astore_1*                       |*...,aref → ...,*                         | 将 *reference* 值从栈顶弹出，并赋值给本地变量表中索引为 *1* 的本地变量            |
| 0x4d |*astore_2*                       |*...,aref → ...,*                         | 将 *reference* 值从栈顶弹出，并赋值给本地变量表中索引为 *2* 的本地变量            |
| 0x4e |*astore_3*                       |*...,aref → ...,*                         | 将 *reference* 值从栈顶弹出，并赋值给本地变量表中索引为 *3* 的本地变量            |
| 0x4f |*iastore*                        |*...,aaref,index,v → ...,*                | 将 *aaref, index (int), v (int)* 从栈顶弹出，并将 *v* 存入 *aaref[index]*         |
| 0x50 |*lastore*                        |*...,aaref,index,v → ...,*                | 将 *aaref, index (int), v (long)* 从栈顶弹出，并将 *v* 存入 *aaref[index]*        |
| 0x51 |*fastore*                        |*...,aaref,index,v → ...,*                | 将 *aaref, index (int), v (float)* 从栈顶弹出，并将 *v* 存入 *aaref[index]*       |
| 0x52 |*dastore*                        |*...,aaref,index,v → ...,*                | 将 *aaref, index (int), v (double)* 从栈顶弹出，并将 *v* 存入 *aaref[index]*      |
| 0x53 |*aastore*                        |*...,aaref,index,v → ...,*                | 将 *aaref, index (int), v (reference)* 从栈顶弹出，并将 *v* 存入 *aaref[index]*   |
| 0x54 |*bastore*                        |*...,aaref,index,v → ...,*                | 将 *aaref, index (int), v (byte)* 从栈顶弹出，并将 *v* 存入 *aaref[index]*        |
| 0x55 |*castore*                        |*...,aaref,index,v → ...,*                | 将 *aaref, index (int), v (char)* 从栈顶弹出，并将 *v* 存入 *aaref[index]*        |
| 0x56 |*sastore*                        |*...,aaref,index,v → ...,*                | 将 *aaref, index (int), v (short)* 从栈顶弹出，并将 *v* 存入 *aaref[index]*       |
| 0x57 |*pop*                            |*...,v → ...,*                            | 将栈顶的值弹出                                                                    |
| 0x58 |*pop2*                           |*...,v2,v1 → ...,*                        | 将栈顶的 1 或 2 个值弹出                                                          |
| 0x59 |*dup*                            |*...,v → ...,v,v*                         | 复制栈顶的值，并将复制的值压入栈顶                                                |
| 0x5a |*dup_x1*                         |*...,v2,v1 → ...,v1,v2,v1*                | 复制栈顶的值，并将复制的值插在栈顶往下的第 2 个位置                               |
| 0x5b |*dup_x2*                         |*...,v3,v2,v1 → ...,v1,v3,v2,v1*          | 复制栈顶的值，并将复制的值插在栈顶往下的第 2 或 3 个位置                          |
| 0x5c |*dup2*                           |*...,v2,v1 → ...,v2,v1,v2,v1*             | 复制栈顶的 1 或 2 个值，并将复制的值按原来的顺序压入栈顶                          |
| 0x5d |*dup2_x1*                        |*...,v3,v2,v1 → ...,v2,v1,v3,v2,v1*       | 复制栈顶的 1 或 2 个值，并将复制的值按原来的顺序插在栈顶往下的第 2 或 3个位置     |
| 0x5e |*dup2_x2*                        |*...,v4,v3,v2,v1 → ...,v2,v1,v4,v3,v2,v1* | 复制栈顶的 1 或 2 个值，并将复制的值按原来的顺序插在栈顶往下的第 2、3 或 4 个位置 |
| 0x5f |*swap*                           |*...,v2,v1 → ...,v1,v2*                   | 交换栈顶的两个值                                                                  |
| 0x60 |*iadd*                           |*...,v1,v2 → ...,result*                  | 将栈顶的两个 *int* 值相加，并将结果压入栈顶                                       |
| 0x61 |*ladd*                           |*...,v1,v2 → ...,result*                  | 将栈顶的两个 *long* 值相加，并将结果压入栈顶                                      |
| 0x62 |*fadd*                           |*...,v1,v2 → ...,result*                  | 将栈顶的两个 *float* 值相加，并将结果压入栈顶                                     |
| 0x63 |*dadd*                           |*...,v1,v2 → ...,result*                  | 将栈顶的两个 *double* 值相加，并将结果压入栈顶                                    |
| 0x64 |*isub*                           |*...,v1,v2 → ...,result*                  | 将栈顶的下一个 *int* 值减栈顶的 *int* 值，并将结果压入栈顶                        |
| 0x65 |*lsub*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x66 |*fsub*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x67 |*dsub*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x68 |*imul*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x69 |*lmul*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x6a |*fmul*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x6b |*dmul*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x6c |*idiv*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x6d |*ldiv*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x6e |*fdiv*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x6f |*ddiv*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x70 |*irem*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x71 |*lrem*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x72 |*frem*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x73 |*drem*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x74 |*ineg*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x75 |*lneg*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x76 |*fneg*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x77 |*dneg*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x78 |*ishl*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x79 |*lshl*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x7a |*ishr*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x7b |*lshr*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x7c |*iushr*                          |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x7d |*lushr*                          |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x7e |*iand*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x7f |*land*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x80 |*ior*                            |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x81 |*lor*                            |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x82 |*ixor*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x83 |*lxor*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x84 |*iinc,AA,+BB[^5]*                |*...,v → ...,result*                      |                                                                                   |
| 0x85 |*i2l*                            |*...,v → ...,result*                      |                                                                                   |
| 0x86 |*i2f*                            |*...,v → ...,result*                      |                                                                                   |
| 0x87 |*i2d*                            |*...,v → ...,result*                      |                                                                                   |
| 0x88 |*l2i*                            |*...,v → ...,result*                      |                                                                                   |
| 0x89 |*l2f*                            |*...,v → ...,result*                      |                                                                                   |
| 0x8a |*l2d*                            |*...,v → ...,result*                      |                                                                                   |
| 0x8b |*f2i*                            |*...,v → ...,result*                      |                                                                                   |
| 0x8c |*f2l*                            |*...,v → ...,result*                      |                                                                                   |
| 0x8d |*f2d*                            |*...,v → ...,result*                      |                                                                                   |
| 0x8e |*d2i*                            |*...,v → ...,result*                      |                                                                                   |
| 0x8f |*d2l*                            |*...,v → ...,result*                      |                                                                                   |
| 0x90 |*d2f*                            |*...,v → ...,result*                      |                                                                                   |
| 0x91 |*i2b*                            |*...,v → ...,result*                      |                                                                                   |
| 0x92 |*i2c*                            |*...,v → ...,result*                      |                                                                                   |
| 0x93 |*i2s*                            |*...,v → ...,result*                      |                                                                                   |
| 0x94 |*lcmp*                           |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x95 |*fcmpl*                          |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x96 |*fcmpg*                          |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x97 |*dcmpl*                          |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x98 |*dcmpg*                          |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x99 |*ifeq,+AAAA*                     |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x9a |*ifne,+AAAA*                     |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x9b |*iflt,+AAAA*                     |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x9c |*ifge,+AAAA*                     |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x9d |*ifgt,+AAAA*                     |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x9e |*ifle,+AAAA*                     |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0x9f |*if_icmpeq,+AAAA*                |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0xa7 |*goto,+AAAA*                     |                                          |                                                                                   |
| 0xa0 |*if_icmpne,+AAAA*                |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0xa1 |*if_icmplt,+AAAA*                |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0xa2 |*if_icmpge,+AAAA*                |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0xa3 |*if_icmpgt,+AAAA*                |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0xa4 |*if_icmple,+AAAA*                |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0xa5 |*if_acmpeq,+AAAA*                |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0xa6 |*if_acmpne,+AAAA*                |*...,v1,v2 → ...,result*                  |                                                                                   |
| 0xa8 |*jsr,+AAAA*                      |*... → ...,address*                       |                                                                                   |
| 0xa9 |*ret,AA*                         |无变化                                    |                                                                                   |
| 0xaa |*tableswitch<br>[0]{0,3}<br>+AAAAAAAA<br>+BBBBBBBB<br>+CCCCCCCC<br>{+DDDDDDDD..+NNNNNNNN}* |*...,index → ...* |                                                 |
| 0xab |*lookupswitch<br>[0]{0,3}<br>+AAAAAAAA<br>+BBBBBBBB<br>+CCCCCCCC<br>{+DDDDDDDD..+NNNNNNNN}*|*...,key → ...*   |                                                 |
| 0xac |*ireturn*                        |*...,v → [empty]*                         |                                                                                   |
| 0xad |*lreturn*                        |*...,v → [empty]*                         |                                                                                   |
| 0xae |*freturn*                        |*...,v → [empty]*                         |                                                                                   |
| 0xaf |*dreturn*                        |*...,v → [empty]*                         |                                                                                   |
| 0xb0 |*areturn*                        |*...,v → [empty]*                         |                                                                                   |
| 0xb1 |*return*                         |*...,v → [empty]*                         |                                                                                   |
| 0xb2 |*getstatic,AAAA*                 |*... → ...,v*                             |                                                                                   |
| 0xb3 |*putstatic,AAAA*                 |*... → ...,v*                             |                                                                                   |
| 0xb4 |*getfield,AAAA*                  |*...,aref → ...,v*                        |                                                                                   |
| 0xb5 |*putfield,AAAA*                  |*...,aref → ...,v*                        |                                                                                   |
| 0xb6 |*invokevirtual,AAAA*             |*...,aref,[arg1,[arg2...]] → ...*         |                                                                                   |
| 0xb7 |*invokespecial,AAAA*             |*...,aref,[arg1,[arg2...]] → ...*         |                                                                                   |
| 0xb8 |*invokestatic,AAAA*              |*...,[arg1,[arg2...]] → ...*              |                                                                                   |
| 0xb9 |*invokeinterface,AAAA,BB,00*     |*...,aref,[arg1,[arg2...]] → ...*         |                                                                                   |
| 0xba |*invokedynamic,AAAA,00,00*       |*...,[arg1,[arg2...]] → ...*              |                                                                                   |
| 0xbb |*new,AAAA*                       |*... → ...,aref*                          |                                                                                   |
| 0xbc |*newarray,AA*                    |*...,count → ...,aaref*                   |                                                                                   |
| 0xbd |*anewarray,AAAA*                 |*...,count → ...,aaref*                   |                                                                                   |
| 0xbe |*arraylength*                    |*...,aaref → ...,length*                  |                                                                                   |
| 0xbf |*athrow*                         |*...,aref → ...,aref*                     |                                                                                   |
| 0xc0 |*checkcast,AAAA*                 |*...,aref → ...,aref*                     |                                                                                   |
| 0xc1 |*instanceof,AAAA*                |*...,aref → ...,result*                   |                                                                                   |
| 0xc2 |*monitorenter*                   |*...,aref → ...*                          |                                                                                   |
| 0xc3 |*monitorexit*                    |*...,aref → ...*                          |                                                                                   |
| 0xc4 |*wide,&lt;opcode&gt;,AAAA,[BBBB]*|同原指令                                  |                                                                                   |
| 0xc5 |*multianewarray,AAAA,BB*         |*...,count1,[count2,...] → ...,aaref*     |                                                                                   |
| 0xc6 |*ifnull,+AAAA*                   |*...,v → ...*                             |                                                                                   |
| 0xc7 |*ifnonnull,+AAAA*                |*...,v → ...*                             |                                                                                   |
| 0xc8 |*goto_w,+AAAAAAAA*               |无变化                                    |                                                                                   |
| 0xc9 |*jsr_w,+AAAAAAAA*                |*... → ...,address*                       |                                                                                   |
| 0xca |*breakpoint*                     |                                          | 为 *Java debugger 预留*                                                           |
| 0xcb |...                              |                                          | 预留                                                                              |
| ...  |...                              |                                          | 预留                                                                              |
| 0xfd |...                              |                                          | 预留                                                                              |
| 0xfe |*impdep1*                        |                                          | 为 debugger 预留                                                                  |
| 0xff |*impdep2*                        |                                          | 为 debugger 预留                                                                  |

----

[^1]: 用于存放操作数的栈结构，JVM 指令在执行的时候会从栈中取操作数，并将结果压回栈顶。栈还用于存放方法的参数（非静态方法的第一个参数是 *this* 引用），以及方法返回的结果。
[^2]: *AA* 表示 1 个无符号字节 *(unsighed byte)*
[^3]: 直接编码在指令中并作为操作数使用的数据，如：`bipush 0x10`，`0x10` 被直接编码进指令序列中，即为立即数。
[^4]: *AAAA* 表示 1 个无符号 16 位整型 *(unsighed 16-bit int)*
[^5]: *+BB* 表示 1 个有符号字节 *(signed byte)*
