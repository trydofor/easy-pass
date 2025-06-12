# Easy Pass 1.0

Easy rules to remember any password.

> English 🇺🇸 | [中文 🇨🇳](readme-zh.md)

## 1.Easy Hint

Just remember the hint string.

### 1.1.Token

* `\` = escape char. escaped as `\\`
* `;` = end of part. escaped as `\;`
* `:` = hint or len. escaped as `\:`
* `|` = pipeline to transform. escaped as `\|`
* `*` = mask N chars. escaped as `\*`

### 1.2.Refer

* `#|` = refer to #th part
* `0|` = refer to the label

### 1.3.Trans

* `a` = only `aeiou`
* `A` = only non-`aeiou`
* `e` = to english spell
* `E` = to Non-English, e.g. Pinyin
* `u` = to lower case
* `U` = to UPPER (non-lower) CASE

### 1.4.Usage

* `dog|aU` = `O`, only `aeiou`, to UPPER
* `dog|AU:2` = `DG`, not `aeiou`, to UPPER, get 2-char
* `dog|U:3` = `DOG`, all to UPPER, get 3-char
* `dog|1:3` = `d7g`, transform, get 3-char
* `dog|U1:3` = `D7G`, to UPPER, transform, get 3-char
* `dog|EU:3` = `GOU`, to Pinyin, to UPPER, get 3-char
* `dog|EIU` = `G`, to Pinyin, keep 1st, to UPPER
* `dashlane: d*|U:3;@;0|U0;` = `DOG@D45HL4N3`

## 2.Easy Hash

Just remember one seed string.

### 2.1.Param

* `_seed` = secret string, e.g. poems 
* `_site` = domain or app-name
* `_user` = username to login
* `_size` = password length
* `mark` = `sha$_size:$_user:$_site` 1-line style
* `echo -n $mark:$_seed | sha1sum | xxd -r -p | base64 | cut -c -$_size`

### 2.2.Shell

```bash
_seed='chuang qian ming yue guang'
## para
_site='gmail.com'
_user='trydofor'
_size=20
## mark
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

## 3.Easy Mage

use `Easy Hint` to remember `Easy Hash` to be a password Mage.

* `Easy Hash` Online <https://easypass.trydofor.com>
