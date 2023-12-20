# Dolby Atmos Bitstream Analysis

This folder includes one ```ATMOSFrame``` extracted from a unlocked Dolby Atmos Cinema MXF essence (extracted with [asdcplib](https://github.com/cinecert/asdcplib)), and a C style pseudo code to show its structure. It aims to prove that IAB Application Profile 1 is equal to Dolby Atmos Bitstream.

This structure was identified with the instructions from ST 2098-2:2019 and RDD57:2021.

## Informative notes

### Steps of analyzing

1. Use ```asdcplib``` tool ```asdcp-unwrap``` to extract the Dolby Atmos Cinema MXF.

```sh
asdcp-unwrap <Input File>.mxf DCPIAB
```

2. Take its second frame ```DCPIAB000002.atmos``` and use a HEX editor to analyse, following the guide from ST 2098-2 and RDD57.

### Pseudo code notes

The pseudo code is roughly C style, but aims to prove the structure. Each symbol was started with a number that tells this symbol takes how many bits. It may quote another symbol's number, or write as ```?``` to announce that we don't care about its size.

Each element was named as "```NameElement()```", included in "```{}```" symbols. The content was named as "```Name()```", included in "```{}```" symbols.

As we are not familiar with DLC lossless coding, we did not analyse ```AudioDataDLC``` element.

For ```ObjectDefinition``` element, as we need to reduce working, we only analyse those whose ```MetaID``` is ```0x01```, ```0x02```, ```0x3A```, ```0x76```, which represents the structure more clearly.

# 杜比全景声比特流分析

这个文件夹包含了一个从未加密Dolby Atmos Cinema MXF精华（使用[asdcplib](https://github.com/cinecert/asdcplib)提取）中提取的一个```ATMOSFrame```，和一个表明它的结构的C风格伪代码，旨在证明IAB应用配置文件1同杜比全景声比特流等价。

这一结构是根据ST 2098-2:2019和RDD57:2021中的指导识别的。

## 信息性备注

### 分析步骤
1. 使用```asdcplib```工具```asdcp-unwrap```提取该Dolby Atmos Cinema MXF。

```sh
asdcp-unwrap <Input File>.mxf DCPIAB
```

2. 取其第二帧```DCPIAB000002.atmos```并遵守ST 2098-2和RDD57的指导，使用十六进制编辑工具对其进行分析。

### 伪代码备注

这个伪代码大致是C语言风格的，但旨在表明结构。每一个符号由一个代表该符号占据多少位的数字开头。它可能引用其它符号的数值，也可能被写作```?```代表不关心其大小。

每一个元素都被命名为“```NameElement()```”，包含在花括号中。内容被命名为“```Name()```”，包含在花括号中。

由于并不熟悉DLC无损音频编码，```AudioDataDLC```元素未被分析。

针对```ObjectDefinition```元素，仅分析了```MetaID```为```0x01```, ```0x02```, ```0x3A```, ```0x76```的四项，以节约工作。
