# go 中 int 和 byte 转换方式

## 主机字节序

主机字节序模式有两种，大端数据模式和小端数据模式，在网络编程中应注意这两者的区别，以保证数据处理的正确性；例如网络的数据是以大端数据模式进行交互，而我们的主机大多数以小端模式处理，如果不转换，数据会混乱 参考 ；一般来说，两个主机在网络通信需要经过如下转换过程：主机字节序 —> 网络字节序 -> 主机字节序。

## 大端小端区别

大端模式：Big-Endian就是高位字节排放在内存的低地址端，低位字节排放在内存的高地址端
低地址 --------------------> 高地址
高位字节                     低位字节
小端模式：Little-Endian就是低位字节排放在内存的低地址端，高位字节排放在内存的高地址端
低地址 --------------------> 高地址
低位字节                     高位字节

## 什么是高位字节和低位字节

例如在32位系统中，357转换成二级制为：00000000 00000000 00000001 01100101，其中

00000001 | 01100101
高位字节    低位字节

## int和byte转换

在go语言中，byte其实是uint8的别名，byte 和 uint8 之间可以直接进行互转。

## 示例

```go
package main

import (
    "bytes"
    "encoding/binary"
    "fmt"
)

func main() {

    var n int64 = 511

    fmt.Println(Int64ToBytes(n))

    var b []byte = []byte{6: 1, 7: 255}

    fmt.Println(BytesToInt64(b))
}

func Int64ToBytes(n int64) []byte {
    bytesBuffer := bytes.NewBuffer([]byte{})
    _ = binary.Write(bytesBuffer, binary.BigEndian, n)
    return bytesBuffer.Bytes()
}

func BytesToInt64(b []byte) int64 {
    bytesBuffer := bytes.NewBuffer(b)
    var x int64
    _ = binary.Read(bytesBuffer, binary.BigEndian, &x)
    return x
}

```
