# 易记密码 1.0

简单规则记住任何密码。

> 中文 🇨🇳 | [English 🇺🇸](readme.md)

## 1.易记暗语

仅需记住一个暗语。

### 1.1.记号

* `\` = 转义符。转义为`\\`
* `;` = 分段的结束。转义为`\;`
* `:` = 暗语或长度。转义为`\:`
* `|` = 用于变形的管道。转义为`\|`
* `*` = 遮罩多个字符。转义为`\*`

### 1.2.引用

* `#|` = 引用第#分段
* `0|` = 引用指定标签

### 1.3.变形

* `a` = 仅留`aeiou`
* `A` = 仅留非`aeiou`
* `e` = 变为英文拼写
* `E` = 变为非英文拼写，如拼音
* `u` = 变为小写
* `U` = 变为大写（非小写）

### 1.4.用法

* `dog|aU` = `O`，仅留`aeiou`，变大写
* `dog|AU:2` = `DG`，移除`aeiou`，变大写，共2字符
* `dog|U:3` = `DOG`，全大写，共3字符
* `dog|1:3` = `d7g`，变形，共3字符
* `dog|U1:3` = `D7G`，变大写，变形，共3字符
* `dog|EU:3` = `GOU`，变拼音，变大写，共3字符
* `dog|EIU` = `G`，变拼音，仅留首字，变大写
* `dashlane: d*|U:3;@;0|U0;` = `DOG@D45HL4N3`

## 2.易记哈希

仅需记住一个种子词句。

### 2.1.参数

* `_seed` = 私密的词句，如名言，诗词等
* `_site` = 网址或应用名
* `_user` = 登录的用户名
* `_size` = 需要的密码长度
* `mark` = `sha$_size:$_user:$_site` 一行表示法
* `echo -n $mark:$_seed | sha1sum | xxd -r -p | base64 | cut -c -$_size`

### 2.2.命令

```bash
_seed='chuang qian ming yue guang'
## 参数
_site='gmail.com'
_user='trydofor'
_size=20
## 一行表示法
mark=sha$_size:$_user:$_site
echo $mark
## sha20:trydofor:gmail.com
echo -n $mark:$_seed | sha1sum
## a53332b953a6fe12991d823af6fea849d9ea48a4
echo -n $mark:$_seed | sha1sum \
| xxd -r -p | base64
## pTMyuVOm/hKZHYI69v6oSdnqSKQ=
echo -n $mark:$_seed | sha1sum \
| xxd -r -p | base64 | cut -c -$_size
## pTMyuVOm/hKZHYI69v6o
```

## 3.易记大师

使用 `易记暗语` 记住 `易记哈希` 成为一个密码大师。

* `易记哈希` 在线 <https://easypass.trydofor.com>
