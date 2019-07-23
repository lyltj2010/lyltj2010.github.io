---
layout: post
title:  换行符
date:   2019-07-23 12:00:00
category: "cs"
keywords: line break, 换行符
---

换行符line break在不同系统中可能会用不同字符表示，简单对比下。

| 类型 | 含义 | 字符表示 | ASCII码 | 系统 |
| --- | --- | --- | --- | --- |
| CR | 移动到行首，不移动下一行 | `\r` | `0x0D` | Early Macintosh OS  |
| LF | 移动到下一行，不移动到行首 | `\n` | `0x0A` | UNIX based |
| CRLF | 移动到下一行，并移动到行首 | `\r\n` | `0x0D 0x0A` | Windows, Symbian OS |

> CR = Carriage Return and LF = Line Feed, two expressions have their roots in the old typewriters / TTY. LF moved the paper up (but kept the horizontal position identical) and CR brought back the "carriage" so that the next character typed would be at the leftmost position on the paper (but on the same line). CR+LF was doing both, i.e. preparing to type a new line.

有时候复制代码，可能遇到`Bash syntax error: unexpected end of file`类似报错，很可能是换行符不一致导致的。可以用doc2unix工具转化`doc2unix filename`。

Refs

+ [Difference between CR LF, LF and CR line break types?](https://stackoverflow.com/questions/1552749/difference-between-cr-lf-lf-and-cr-line-break-types)
+ [Bash syntax error: unexpected end of file](https://stackoverflow.com/questions/6366530/bash-syntax-error-unexpected-end-of-file/6366607)




