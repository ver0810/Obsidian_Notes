---
id: shell
aliases:
  - shell
tags: []
---

# shell

### 重定向

一般情况下命令从标准输入（stdin）读取输入，并输出到标准输出（stdout），默认情况下两者都是你的终端。使用重定向可以让命令从文件读取输入/输出到文件。下面是以 echo 为例的重定向输出：

无论是 > 还是 >>，当输出文件不存在时都会创建该文件。

重定向输入使用符号 <：

command < inputfile
command < inputfile > outputfile

速度发