

写代码这么久，突然发现并不了解字符编码。我们每天写下的代码，或者文件，在计算机中究竟是怎样的存在？我们都知道，计算机能够认识的只有 `0` 和 `1`。所以，不论任何数据，最终在计算机中只是 `0` 和 `1` 的排列组合。那么计算机时如何识别这些排列组合的呢？这就需要 `字符编码（Character encoding）`了。简单的说，就是按照一定的规则将信息与其对应的 `0` 和 `1` 的排列组合对应起来，这样计算机就可以根据字符编码识别出硬盘中的排列组合所代表的真实信息了。常见的 `ASCII` `UTF-8` `GBK` 等等，都是典型的字符编码。计算机到底是如何辨别这些字符编码的，就要看一下具体的字符编码原理。

# ASCII

**ASCII（American Standard Code for Information Interchange，美国信息交换标准代码）**，是基于拉丁字母的一套电脑编码系统。注意最后两个字母是 `II`，而不是罗马数字 2。`ASCII` 是由美国国家标准协会制定的，标准的单字节字符编码方案，用于基本文本的数据。起源于 50 年代后期，在 1967 年定案。它最初是美国国家标准，供不同计算机在相互通信时用作共同遵守的西文字符编码标准，它已被国际标准化组织定为国际标准，称为 ISO 646 标准。适用于所有拉丁文字字母。

标准 `ASCII` 码使用单字符，即 `8` 个二进制位表示字符。第一位统一定为 `0`，实际使用后面 `7` 位来表示，所以 `ASCII` 码一共规定了 `128` 个字符的编码，包括所有的大小写字母，数字 0 到 9，标点符号以及一些特殊控制字符。

标准 ASCII 码表如下：

![](https://user-gold-cdn.xitu.io/2018/2/8/16175c2c1337feb8?w=715&h=488&f=gif&s=28002)

`ASCII` 是美国标准，并不能满足其他语言的需求。例如英镑符号，中文汉字等等。西方一些国家使用 `8` 个二进制位来表示字符，最多可以表示 `256` 个字符。显然，对于汉字而言，一个字符不可能满足需求。

# ANSI

为了扩充 `ASCII` 编码，以用于显示本国的语言，不同的国家和地区制定了不同的标准，由此产生了 `GB2312` , `BIG5` , `JIS` 等各自的编码标准。这些使用 `2` 个字节来代表一个字符的各种汉字延伸编码方式，称为 `ANSI` 编码，又称为 `MBCS（Muilti-Bytes Charecter Set，多字节字符集）`。在简体中文系统下，ANSI 编码代表 `GB2312` 编码，在日文操作系统下，`ANSI` 编码代表 `JIS` 编码，所以在中文 windows下要转码成 `gb2312` , `gbk` 只需要把文本保存为 `ANSI 编码` 即可。不同的 `ANSI` 编码并不兼容，同一个二进制值在不同的编码体系中可能代表不同的字，这就导致了 `Unicode` 的诞生。在介绍 `Unicode` 之前，简单看一下 `ANSI` 中的中文编码。

## GB2313

`GB2312` 也是 `ANSI` 编码里的一种，对 `ANSI` 编码最初始的 `ASCII` 编码进行扩充，为了满足国内在计算机中使用汉字的需要，中国国家标准总局发布了一系列的汉字字符集国家标准编码，统称为 `GB码` ，或国标码。其中最有影响的是于 1980 年发布的《信息交换用汉字编码字符集 基本集》，标准号为 `GB 2312-1980` ,因其使用非常普遍，也常被通称为国标码。`GB2312` 编码通行于我国内地；新加坡等地也采用此编码。几乎所有的中文系统和国际化的软件都支持 `GB 2312`。

`GB2312` 是一个简体中文字符集，由 `6763` 个常用汉字和 `682` 个全角的非汉字字符组成。其中汉字根据使用的频率分为两级。一级汉字 `3755` 个，二级汉字 `3008` 个。

## GBK

`GB2312` 的出现，基本满足了汉字的计算机处理需要，但是对于人名，古汉语等方面的罕用字，`GB2312` 不能处理，这就导致了 `GBK` 的出现。

`GBK` 采用双字节表示，总体编码范围为 `8140-FEFE` ，首字节在 `81-FE` 之间，尾字节在 `40-FE` 之间，剔除 `xx7F` 一条线。总计 `23940` 个码位，共收入 `21886` 个汉字和图形符号，其中汉字（包括部首和构件）`21003` 个，图形符号 `883` 个。

# Unicode

`ANSI` 编码的缺点很明显，同一个编码值，在不同的编码体系中代表着不同的字符，很容易造成乱码。如果有一种编码，将世界上所有的符号都融入其中，每个符号都有对应的编码值，这样就不存在乱码问题了。这就是 `Unicode` 编码。

`Unicode` 编码是一个很大的集合，现在的规模可以容纳 100 多万个符号，每个符号的编码都不一样。其实 `Unicode` 并不是真正意义上的字符编码，它只是一个字符集，规定了符号的二进制码，却没有规定这个二进制码应该如何存储。`Unicode` 有一些具体的实现编码，其中用途最广泛的莫属 `UTF-8`。

# UTF-8

`UTF-8` 是使用最广的 `Unicode` 的一种 **Unicode 的实现方式** ，它是一种变长的编码方式，使用 1 ~ 4 个字符表示一个符号，根据不同的符号而变化字符长度，提高了 Unicode 的编码效率。先来看一下 `UTF-8` 对于不同字节数的符号的表示方法, `x` 代表可使用的二进制位：

字节数 | 编码规则 | 可表示字符数量
- | :- | :-
1 字节 | 0xxxxxxx | 2的7次方 = 128
2 字节 | 11xxxxxx 10xxxxxx | 2的11次方 = 2048
3 字节 | 1110xxxx 10xxxxxx 10xxxxxx| 2的15次方 = 65536
4 字节 | 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx| 2的21次方 = 4194304

由上面的表很容易发现 `UTF-8` 的编码规则：

* 对于单字节符号，第一位为 `0`，后面 `7` 为表示这个符号的 `Unicode码`。所以对于单字节符号，`UTF-8` 的表示方式与 `ASCII` 一致。

* 对于 `n` 字节的符号，第一个字节的前 `n` 位都为 `1`，第 `n+1` 位为 `0`，后面的所有字节前两位均为 `10`，剩下的二进制位为这个字符的 `Unicode码`。

使用这种变长编码方式，对于单字节的符号仅需使用一个字节来表示，不会造成浪费。对于汉字来说，一般都是使用三个字符来表示。对于计算机来说，也很容易区分一个字符到底占用几个字节：

* 如果一个字节的第一位为 `0`，这个字节就是一个字符
* 如果第一位为 `1`，连续有多少个 `1`，就表示当前字符占用多少个字节

除了 `UTF-8`，相应的还有 `UTF-16`。在 `UTF-8` 中，以 `8` 个二进制位表示一个字符，而在 `UTF-16` 中，以 `16` 个二进制位表示一个字符。`16` 个二进制位可以直接表示 `65536` 个字符，所以在 `UTF-16` 中，汉字和英文字母具有同样的地位，都是使用 `16` 个二进制位，即 `2` 个字节表示 `1` 个字符。对英文来说会造成浪费，但是对中文来说，可以节省存储空间。

关于字符编码，应该有了一个大概的认识，在日常使用中，我们要尽量做到编码的统一，避免出现乱码的情况。

参考文章：

* [字符编码笔记：ASCII，Unicode 和 UTF-8](http://www.ruanyifeng.com/blog/2007/10/ascii_unicode_and_utf-8.html)
* [UTF-8为什么会比UTF-16浪费？](https://segmentfault.com/a/1190000012692022?utm_source=weekly&utm_medium=email&utm_campaign=email_weekly)
* [谈谈Unicode编码](http://www.pconline.com.cn/pcedu/empolder/gj/other/0505/616631.html)

> 文章同步更新于微信公众号： **`秉心说`** ， 专注 Java 、 Android 原创知识分享，LeetCode 题解，欢迎关注！

![](https://user-gold-cdn.xitu.io/2019/3/25/169b27943f1fcc1f?w=258&h=258&f=jpeg&s=27909)