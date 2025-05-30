# 文本编码

Evennia 是一个基于文本的游戏服务器，因此理解它如何处理文本形式的数据非常重要。

文本的*字节编码*描述了文本字符串在计算机中的实际存储方式，即用于表示特定字母表的字节序列。英语中常用的编码是 *ASCII* 编码，它描述了英文字母（Aa-Zz）以及一些特殊字符。对于其他字符集（如包含非英语字母的其他语言），使用诸如 *Latin-1*、*ISO-8859-3* 和 *ARMSCII-8* 等名称的编码。全球使用的字节编码有数百种。

在字节编码中，字母串用 `bytes` 类型表示。与字节编码相对的是*Unicode 表示*，在 Python 中为 `str` 类型。Unicode 是一个国际公认的表格，描述了几乎所有可打印的字母，从英语到中文字母以及介于两者之间的所有字符。因此，Evennia（以及 Python 和 Django）在内部将所有内容存储为 Unicode，但在向用户输出数据时会将其转换为某种编码。

一个简单的记忆方法是，`bytes` 是通过网络传输的内容。在其他所有时候，使用 `str`（Unicode）。这意味着我们必须在发送/接收网络数据时进行两者之间的转换。

问题在于，当通过网络接收到一串字节时，Evennia 无法猜测使用了哪种编码——它只是一堆字节！Evennia 必须知道编码才能正确地转换为 Unicode 表示。

## 如何自定义编码

只要使用标准的 ASCII 字符集（基本上是普通的英文字母），就不必太担心这一部分。

然而，如果你想用其他语言构建游戏，或者预计用户会使用 ASCII 之外的特殊字符，就需要考虑支持哪些编码。

如前所述，全球使用的字节编码有很多种。显然，Evennia 无法猜测，而是必须假设或以某种方式被告知你想用哪种编码与服务器通信。基本上，客户端使用的编码必须与服务器使用的编码相同。这可以通过两种互补的方式进行自定义。

1. 指导用户使用默认的 `@encoding` 命令或 `@options` 命令。这允许他们自己设置所使用的编码（以及他们选择的客户端）。虽然数据在 Evennia 内部仍然存储为 Unicode 字符串，但从该玩家接收和发送的所有数据在传输前都会转换为给定格式。
   
2. 作为备份，以防用户设置的编码转换出错或以其他方式失败，Evennia 将回退尝试使用设置变量 `ENCODINGS` 中定义的名称。这是 Evennia 在放弃并给出编码错误消息之前尝试的一系列编码名称。

请注意，每次输入/输出都尝试多种不同编码会增加不必要的开销。尽量猜测玩家最常用的编码，并确保首先尝试这些编码。国际 *UTF-8* 编码是 Evennia 默认假设的编码（也是 Python/Django 通常使用的编码）。有关更多帮助，请参阅维基百科文章[这里](https://en.wikipedia.org/wiki/Text_encodings)。
