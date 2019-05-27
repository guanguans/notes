# PHP 常用函数

## [](#String "String")String

### [](#比较 "比较")比较

| 函数名 | 描述 |
| --- | --- |
| strcmp | 该函数是二进制安全的，且对大小写敏感 |
| strncmp | 前 n 个字符的字符串比较（对大小写敏感） |
| strcasecmp | 比较两个字符串，对大小写不敏感 |
| strncasecmp | 前 n 个字符的字符串比较（对大小写不敏感） |
| strnatcmp | 使用一种 “自然” 算法来比较两个字符串（对大小写敏感） |
| strnatcasecmp | 使用一种 “自然” 算法来比较两个字符串（对大小写不敏感） |
| substr_compare | 从指定的开始长度比较两个字符串 |
| strcoll | 该函数不是二进制安全的，对大小写敏感；字符串的比较会根据本地设置而变化。（A<a 或="" a="">a）</a> |

### [](#修改 "修改")修改

| 函数名 | 描述 |
| --- | --- |
| str_repeat | 把字符串重复指定的次数 |
| strrev | 反转字符串 |
| str_shuffle | 随机地打乱字符串中的所有字符 |
| wordwrap | 按照指定长度对字符串进行折行处理 |
| chunk_split | 把字符串分割为一连串更小的部分 |
|  |  |
| money_format | 把字符串格式化为货币字符串 |
| number_format | 通过千位分组来格式化数字 |
|  |  |
| str_pad | 把字符串填充为指定的长度 |
|  |  |
| strtolower | 把字符串转换为小写 |
| strtoupper | 把字符串转换为大写 |
| lcfirst | 把字符串中的首字符转换为小写 |
| ucfirst | 把字符串中的首字符转换为大写 |
| ucwords | 把字符串中每个单词的首字符转换为大写 |
|  |  |
| strtr | 转换字符串中特定的字符 |
| str_replace | 使用一个字符串替换字符串中的另一些字符（对大小写敏感） |
| str_ireplace | 替换字符串中的一些字符。（对大小写不敏感） |
| substr_replace | 函数把字符串的一部分替换为另一个字符串 |
|  |  |
| hebrev | 把希伯来逻辑文本转换为希伯来可见文本 |
| hebrevc | 把希伯来逻辑文本转换为希伯来可见文本，把新行 (`\n`) 转换为 `<br />` |
| convert_cyr_string | 把字符串由一种 Cyrillic 字符集转换成另一种 |

### [](#插入 "插入")插入

| 函数名 | 描述 |
| --- | --- |
| addslashes | 在指定的预定义字符前添加反斜杠，可用于为存储在数据库中的字符串以及数据库查询语句准备合适的字符串 |
| stripslashes | 删除由 `addslashes()` 函数添加的反斜杠 |
| addcslashes | 在指定的字符前添加反斜杠 |
| stripcslashes | 删除由 `addcslashes()` 函数添加的反斜杠 |
| quotemeta | 在字符串中某些预定义的字符前添加反斜杠 |

### [](#删除 "删除")删除

| 函数名 | 描述 |
| --- | --- |
| trim | 从字符串的两端删除空白字符和其他预定义字符 |
| chop | `rtrim()` 的别名 |
| ltrim | 从字符串左侧删除空格或其他预定义字符 |
| rtrim | 从字符串的末端开始删除空白字符或其他预定义字符 |

### [](#子字符串 "子字符串")子字符串

| 函数名 | 描述 |
| --- | --- |
| substr | 返回字符串的一部分 |
| strrchr | 查找字符串在另一个字符串中最后一次出现的位置，并返回从该位置到字符串结尾的所有字符 |
| strtok | 按需切割字串，不可以用中文切割会乱码 |

### [](#搜索 "搜索")搜索

| 函数名 | 描述 |
| --- | --- |
| strchr | `strstr` 的别名 |
| strstr | 搜索一个字符串在另一个字符串中的第一次出现，返回的是字符串的其余部分（从匹配点），对大小写敏感 |
| stristr | 搜索一个字符串在另一个字符串中的第一次出现，返回的是字符串的其余部分（从匹配点），对大小写不敏感 |
| strpos | 返回字符串在另一个字符串中第一次出现的位置， 返回匹配点位置，对大小写敏感 |
| stripos | 返回字符串在另一个字符串中第一次出现的位置， 返回匹配点位置，对大小写不敏感 |
| strrpos | 返回字符串在另一个字符串中最后一次出现的位置， 返回匹配点位置，对大小写敏感 |
| strripos | 返回字符串在另一个字符串中最后一次出现的位置， 返回匹配点位置，对大小写不敏感 |
|  |  |
| strpbrk | 在字符串中搜索指定字符中的任意一个，对大小写敏感 |

### [](#与数组相关 "与数组相关")与数组相关

| 函数名 | 描述 |
| --- | --- |
| join | `implode()` 的别名 |
| implode | 把数组元素组合为一个字符串 |
| explode | 把字符串打散为数组 |
| str_split | 把字符串分割到数组中 |

### [](#解析 "解析")解析

| 函数名 | 描述 |
| --- | --- |
| parse_str | 把查询字符串解析到变量中 |
| sscanf | 根据指定的格式解析来自一个字符串的输入 |
| str_getcsv | 解析 `CSV` 格式字段的字符串，并返回一个包含所读取字段的数组 |

### [](#与-Html-相关 "与 Html 相关")与 Html 相关

| 函数名 | 描述 |
| --- | --- |
| html_entity_decode | 是 `htmlentities()` 的反函数，把 `HTML` 实体转换为字符 |
| htmlentities | 把字符转换为 `HTML` 实体 |
| htmlspecialchars_decode | 把一些预定义的 `HTML` 实体转换为字符 |
| htmlspecialchars | 把一些预定义的字符转换为 `HTML` 实体 |
| nl2br | 在字符串中的每个新行 (`\n`) 之前插入 `HTML` 换行符 (`<br />`) |
| strip_tags | 剥去 `HTML`、`XML` 以及 `PHP` 的标签 |

### [](#与ASCII相关 "与ASCII相关")与 ASCII 相关

| 函数名 | 描述 |
| --- | --- |
| ord | 返回字符串第一个字符的 `ASCII` 值 |
| chr | 从指定的 `ASCII` 值返回字符 |

### [](#长度、计算 "长度、计算")长度、计算

| 函数名 | 描述 |
| --- | --- |
| strlen | 返回字符串的长度 |
| str_word_count | 计算字符串中的单词数 |
| substr_count | 计算子串在字符串中出现的次数 |
| count_chars | 返回字符串所用字符的信息 |
| strcspn | 返回在找到任何指定的字符之前，在字符串查找的字符数 |
|  |  |
| strspn | 返回在字符串中包含 `charlist` 参数中指定字符的数目 |
|  |  |
| md5_file | 计算文件的 `MD5` 散列 |
| md5 | 计算字符串的 `MD5` 散列 |
| crc32 | 计算一个字符串的 `crc32` 多项式，该函数可用于验证数据的完整性 |
| sha1_file | 计算文件的 `SHA-1` 散列 |
| sha1 | 计算字符串的 `SHA-1` 散列 |
| soundex | 计算字符串的 `soundex` 键，为发音相似的单词创建相同的键 |
| metaphone | 计算字符串的 `metaphone` 键，`metaphone` 键字符串的英语发音 |
|  |  |
| levenshtein | 返回两个字符串之间的 `Levenshtein` 距离 |
| similar_text | 计算两个字符串的匹配字符的数目 |

### [](#输出 "输出")输出

| 函数名 | 描述 |
| --- | --- |
| echo | 同`printf`，比`printf`快【`echo(strings)`】 |
| print | 输出一个字符串【`print()` 函数实际上不是函数，所以不必对它使用括号】【 `print(strings)`】 |
| printf | 输出格式化的字符串 【`printf(format,arg1,arg2,arg++)`】 |
| vprintf | 输出格式化的字符串，与`printf`不同的是第二参数为数组【`vprintf(format,argarray)`】 |
| sprintf | 返回格式化的字符串【`sprintf(format,arg1,arg2,arg++)`】 |
| vsprintf | 返回格式化的字符串，与`sprintf`不同的是第二参数为数组【`vsprintf(format,argarray)`】 |
| fprintf | 把格式化的字符串写到指定的输出流【`fprintf(stream,format,arg1,arg2,arg++)`】 |
| vfprintf | 把格式化的字符串写到指定的输出流【`vfprintf(stream,format,argarray)`】 |

### [](#编码解码、校验 "编码解码、校验")编码解码、校验

| 函数名 | 描述 |
| --- | --- |
| crypt | 单向加密 |
| str_rot13 | 对字符串执行 `ROT13` 编码 |
| convert_uudecode | 对 `uuencode` 编码的字符串进行解码 |
| convert_uuencode | 使用 `uuencode` 算法对字符串进行编码 |
| quoted_printable_decode | 把 `quoted-printable` 字符串解码为 8 位 `ASCII` 字符串 |
| quoted_printable_encode | 把 8 位字符串转换为 `quoted-printable` 字符串 |
|  |  |
| bin2hex | 将二进制数据转换成十六进制表示 |
| hex2bin | 把十六进制值转换为 `ASCII` 字符 |

### [](#配置信息 "配置信息")配置信息

| 函数名 | 描述 |
| --- | --- |
| nl_langinfo | 返回指定的本地信息 |
| setlocale | 设置地区信息（地域信息） |
| localeconv | 包含本地数字及货币信息格式的数组 |
| get_html_translation_table | 返回被 `htmlentities()` 和 `htmlspecialchars()` 函数使用的翻译表 |

## [](#Array "Array")Array

### [](#新建 "新建")新建

| 函数名 | 描述 |
| --- | --- |
| array | 新建一个数组 |
| compact | 建立一个数组，包括变量名和它们的值 |
| array_rand | 返回给定数组中的随机键名 |
| array_fill | 用给定的值填充数组 |
| array_fill_keys | 用给定的指定键名的键值填充数组 |
| array_pad | 指定数量的带有指定值的元素插入到数组中 |
| range | 创建一个包含指定范围的元素的数组 |
| array_combine | 通过合并两个数组来创建一个新数组，其中的一个数组元素为键名，另一个数组元素为键值 |
| array_column | 返回数组中指定的一列 |
| array_chunk | 把数组分割为新的数组块，其中每个数组的单元数目由 `size` 参数决定 |

### [](#返回新数组 "返回新数组")返回新数组

| 函数名 | 描述 |
| --- | --- |
| array_slice | 数组中根据条件取出一段值，并返回 (`key`为数字，删；非数字，保留) |
| array_splice | 从数组中移除选定的元素，并用新元素取代它。该函数也将返回包含被移除元素的数组 (删) |

### [](#赋值 "赋值")赋值

| 函数名 | 描述 |
| --- | --- |
| list | 把数组中的值赋给一些变量 |
| extract | 使用数组键名作为变量名，使用数组键值作为变量值 |

### [](#键或值 "键或值")键或值

| 函数名 | 描述 |
| --- | --- |
| array_keys | 返回包含数组中所有键名的一个新数组 |
| array_key_exists | 检查某个数组中是否存在指定的键名，如果键名存在则返回 `true` |
| key_exists | `array_key_exists` 函数的别名 |
| array_change_key_case | 将数组的所有的键转换为大写字母 |
| array_replace | 根据`Key`, 使用后面数组的值替换第一个数组的值 |
| array_replace_recursive | 递归地使用后面数组的值替换第一个数组的值 |
|  |  |
| array_values | 返回一个包含给定数组中所有键值的数组，但不保留键名 |
| array_unique | 移除数组中的重复的值，并返回结果数组，返回的数组中键名不变 |
|  |  |
| array_flip | 返回一个键值反转后的数组，如果同一值出现了多次，则最后一个键名将作为它的值，所有其他的键名都将丢失 |

### [](#搜索-1 "搜索")搜索

| 函数名 | 描述 |
| --- | --- |
| in_array | 搜索数组中是否存在指定的值 |
| array_search | 在数组中搜索某个键值，并返回对应的键名 |

### [](#进出 "进出")进出

| 函数名 | 描述 |
| --- | --- |
| array_shift | 删除数组中第一个元素，并返回被删除元素的值 (`key`为数字，删；非数字，保留) |
| array_unshift | 向数组插入新元素。新数组的值将被插入到数组的开头 (`key`为数字，删；非数字，保留) |
| array_pop | 删除数组中的最后一个元素 |
| array_push | 向第一个参数的数组尾部添加一个或多个元素（入栈），然后返回新数组的长度 |

### [](#排序 "排序")排序

| 函数名 | 描述 |
| --- | --- |
| shuffle | 把数组中的元素按随机顺序重新排列 (删除`Key`) |
| array_reverse | 返回一个单元顺序相反的数组 (可保留，可删除，由第二参数决定) |
| array_multisort | 对多个数组或多维数组进行排序 (`key`为数字，删；非数字，保留) |
|  |  |
| sort | 按升序对给定数组的值排序 (删除`Key`) |
| rsort | 按降序对给定数组的值排序 (删除`Key`) |
|  |  |
| asort | 对关联数组按照键值进行升序排序 (保留`Key`) |
| arsort | 对关联数组按照键值进行降序排序 (保留`Key`) |
| ksort | 对关联数组按照键名进行升序排序 (保留`Key`) |
| krsort | 对关联数组按照键名进行降序排序 (保留`Key`) |
| natsort | 用” 自然排序” 算法对数组进行排序 (保留`Key`) |
| natcasesort | 用 “自然排序” 算法对数组进行不区分大小写字母的排序(保留`Key`) |
|  |  |
| usort | 使用用户自定义的比较函数对数组中的元素进行排序 (删除`Key`) |
| uksort | 使用用户自定义的比较函数对数组 中的元素按键名进行排序 (保留`Key`) |
| uasort | 使用用户自定义的比较函数对数组中的值进行排序并保持索引关联 (保留`Key`) |

### [](#交集和差集，-合并 "交集和差集， 合并")交集和差集， 合并

| 函数名 | 描述 |
| --- | --- |
| array_diff | 返回所有在被比较的数组中，但是不在任何其他参数数组中的键值。（保留`key`） |
| array_udiff | 比较两个数组的键值（使用用户自定义函数比较键值），并返回差集 |
| array_diff_key | 比较键值，返差集；（保留`key`） |
| array_diff_ukey | 用户定义的比较函数比较键值，返差集；（保留`key`） |
| array_diff_assoc | 返回所有在被比较的数组中，但是不在任何其他参数数组中的键和值（保留`key`） |
| array_udiff_assoc | 同`diff_assoc`比，多了自定义回调函数（参数为键值） |
| array_diff_uassoc | 相比`diff_assoc`，使用的是用户自定义的比较函数（参数为键名） |
| array_udiff_uassoc | 相比`diff_uassoc`，多了两个回调函数，分别用于键名和键值的比较 |
|  |  |
| array_intersect | 比较两个（或更多个）数组的键值，并返回交集数组（保留被比较数组的`key`） |
| array_uintersect | 用自定义回调函数（参数为键值）比较交集 |
| array_intersect_key | 比较键名计算数组的交集（保留被比较数组的`key`） |
| array_intersect_ukey | 用回调函数比较键名来计算数组的交集（保留被比较数组的`key`） |
| array_intersect_assoc | 比较两个数组的键名和键值，并返回交集 |
| array_uintersect_assoc | 同`intersect_assoc`比，多了自定义回调函数（参数为键值） |
| array_intersect_uassoc | 用回调函数比较两个数组的键名和键值，并返回交集 |
| array_uintersect_uassoc | 相比`intersect_uassoc`，多了两个回调函数，分别用于键名和键值的比较 |
|  |  |
| array_merge | 把一个或多个数组合并为一个数组 (`key`为数字，重新排序；非数字，替换) |
| array_merge_recursive | `array_merge_recursive()`不会进行键名覆盖，而是将多个相同键名的值递归组成一个数组 |

### [](#数学运算 "数学运算")数学运算

| 函数名 | 描述 |
| --- | --- |
| count | 返回数组中元素的数目 |
| sizeof | 同`count` |
| array_sum | 返回数组中所有值的和 |
| array_count_values | 统计数组中所有的值出现的次数，数组中的值作为键名，出现的次数作为值 |
| array_product | 计算数组中所有值的乘积 |
| array_map | 将函数作用到数组中的每个值上，每个值都乘以本身，并返回带有新值的数组 |

### [](#内部指针 "内部指针")内部指针

| 函数名 | 描述 |
| --- | --- |
| currrent | 返回数组中的当前单元 |
| pos | 返回数组中的当前单元，同`current`函数 |
| end | 将数组的内部指针指向最后一个单元，并返回指向的单元 |
| next | 将数组中的内部指针向前移动一位，并返回指向的单元 |
| prev | 将数组的内部指针倒回一位，并返回指向的单元 |
| reset | 将数组的内部指针指向第一个单元，并返回指向的单元（即第一个单元） |
| each | 返回数组中当前的键／值对并将数组指针向前移动一步 |
| key | 返回数组中内部指针指向的当前单元的键名。 但它不会移动指针 |

### [](#用户自定义函数 "用户自定义函数")用户自定义函数

| 函数名 | 描述 |
| --- | --- |
| array_walk | 对数组中的每个元素应用用户自定义函数 |
| array_walk_recursive | 该函数与 `array_walk()`函数的不同在于可以操作更深的数组（一个数组中包含另一个数组） |
| array_reduce | 向用户自定义函数发送数组中的值，并返回一个字符串 |
| array_filter | 用回调函数过滤数组中的单元 (数组的键名保留不变) |

## [](#Math "Math")Math

### [](#常用计算 "常用计算")常用计算

| 函数名 | 描述 |
| --- | --- |
| min | 找出最小值 |
| max | 找出最大值 |
| abs | 绝对值 |
|  |  |
| round | 对浮点数进行四舍五入 |
| ceil | 返回大于或者等于指定表达式的最小整数，天花板函数 |
| floor | 返回小于或者等于指定表达式的最大整数，地板函数 |
|  |  |
| intdiv | 对除法结果取整，返回商 |
| fmod | 返回除法的浮点数余数，返回余数 |
|  |  |
| is_nan | 判断是否为合法数值 |
| hypot | 计算一直角三角形的斜边长度 |
| sqrt | 平方根 |

### [](#角度、弧度 "角度、弧度")角度、弧度

| 函数名 | 描述 |
| --- | --- |
| pi | 得到圆周率值 |
| deg2rad | 将角度转换为弧度 |
| rad2deg | 将弧度数转换为相应的角度数 |

### [](#进制转换 "进制转换")进制转换

| 函数名 | 描述 |
| --- | --- |
| base_convert | 在任意进制之间转换数字 |
| decbin | 十进制转换为二进制 |
| bindec | 二进制转换为十进制 |
|  |  |
| decoct | 十进制转换为八进制 |
| octdec | 八进制转换为十进制 |
|  |  |
| dechex | 十进制转换为十六进制 |
| hexdec | 十六进制转换为十进制 |

### [](#随机数 "随机数")随机数

| 函数名 | 描述 |
| --- | --- |
| lcg_value | 组合线性同余发生器，返回范围为 (0, 1) 的一个伪随机数 |
| rand | 产生一个随机整数，如果没有提供可选参数 `min` 和 `max`，`rand()` 返回 0 到 `RAND_MAX` 之间的伪随机整数。 |
| mt_rand | 生成更好的随机整数 |
| getrandmax | 显示随机数最大的可能值 |
| mt_getrandmax | 显示随机数的最大可能值 |
|  |  |
| srand | 播下随机数发生器种子，自 `PHP 4.2.0` 起，不再需要用 `srand()` 或 `mt_srand()` 函数给随机数发生器播种，现在已自动完成 |
| mt_srand | 播下一个更好的随机数发生器种子 (`Mersenne Twister`) |

### [](#对数 "对数")对数

| 函数名 | 描述 |
| --- | --- |
| log | 自然对数 |
| log10 | 以 `10` 为底的对数 |
| log1p | 返回 `log(1 + number)`，甚至当 `number` 的值接近零也能计算出准确结果 |

### [](#指数 "指数")指数

| 函数名 | 描述 |
| --- | --- |
| exp | 计算 `e` 的指数 |
| expm1 | 返回 `exp(number) - 1`，甚至当 `number` 的值接近零也能计算出准确结果 |
| pow | 指数表达式 |

### [](#正切正弦余弦 "正切正弦余弦")正切正弦余弦

| 函数名 | 描述 |
| --- | --- |
| tan | 正切 |
| atan | 反正切 |
| tanh | 双曲正切 |
| atanh | 反双曲正切 |
| atan2 | 两个参数的反正切 |
|  |  |
| sin | 正弦 |
| asin | 反正弦 |
| sinh | 双曲正弦 |
| asinh | 反双曲正弦 |
|  |  |
| cos | 余弦 |
| acos | 反余弦 |
| cosh | 双曲余弦 |
| acosh | 反双曲余弦 |

### [](#有限值、无限值 "有限值、无限值")有限值、无限值

| 函数名 | 描述 |
| --- | --- |
| is_finite | 判断是否为有限值 |
| is_infinite | 判断是否为无限值 |

## [](#Directory "Directory")Directory

### [](#文件夹，获取目录信息 "文件夹，获取目录信息")文件夹，获取目录信息

| 函数名 | 描述 |
| --- | --- |
| dir | 打开一个目录句柄，并返回一个对象。这个对象包含三个方法：`read()` , `rewind()` 以及 `close()` |
| opendir | 打开一个目录句柄，，并返回该句柄。可由 `closedir()`，`readdir()` 和 `rewinddir()` 使用 |
| rewinddir | 倒回目录句柄 |
|  |  |
| getcwd | 取得当前工作目录 |
| scandir | 列出指定路径中的文件和目录 |
| chdir | 把当前的目录改变为指定的目录。若成功，则该函数返回 `true`，否则返回 `false` |
| chroot | 把当前进程的根目录改变为指定的目录。若成功，则该函数返回 `true`，否则返回 `false` |

### [](#文件夹，读 "文件夹，读")文件夹，读

| 函数名 | 描述 |
| --- | --- |
| readdir | 从目录句柄中读取条目 |

### [](#文件夹，关 "文件夹，关")文件夹，关

| 函数名 | 描述 |
| --- | --- |
| closedir | 关闭目录句柄 |

## [](#FileSystem "FileSystem")FileSystem

### [](#创建 "创建")创建

| 函数名 | 描述 |
| --- | --- |
| tmpfile | 建立一个临时文件 |
| tempnam | 建立一个具有唯一文件名的文件。在指定目录中建立一个具有唯一文件名的文件。如果该目录不存在，`tempnam()` 会在系统临时目录中生成一个文件，并返回其文件名。 |
| mkdir | 新建目录 |

### [](#获取文件信息 "获取文件信息")获取文件信息

| 函数名 | 描述 |
| --- | --- |
| fileatime | 取得文件的上次访问时间。如果出错则返回 `false`。时间以 `Unix` 时间戳的方式返回 |
| filectime | 取得文件的 `inode` 修改时间。如果出错则返回 `false`。时间以 `Unix` 时间戳的方式返回 |
| filemtime | 取得文件内容修改时间。若成功，则时间以 `Unix` 时间戳的方式返回。若失败，则返回 `false` |
| fileinode | 取得文件的 `inode`编号 |
| filegroup | 取得文件的组`ID` |
| fileowner | 取得文件的所有者 |
| fileperms | 取得文件的权限 |
| filesize | 取得文件大小 |
| filetype | 取得文件类型 |
| basename | 返回路径中的文件名部分 |
| dirname | 返回路径中的目录部分 |
| realpath | 返回规范化的绝对路径名 |
| stat | 获取指定文件的统计信息。 |
| fstat | 通过已打开的文件指针取得文件信息 |
| pathinfo | 返回文件路径的信息 |
| disk_free_space | 返回目录中的可用空间 |
| diskfreespace | `disk_free_space` 的别名 |
| disk_total_space | 返回一个目录的磁盘总大小 |
| realpath_cache_get | Get realpath cache entries |
| realpath_cache_size | Get realpath cache size |

### [](#改变 "改变")改变

| 函数名 | 描述 |
| --- | --- |
| chgrp | 改变文件所属的组 |
| chmod | 改变文件权限 |
| chown | 改变文件的所有者 |
| touch | 设定文件的访问和修改时间 |
| umask | 改变当前的 umask |
| rename | 重命名一个文件或目录 |
| ftruncate | 将文件截断到给定的长度 |
| flock | 锁定或释放文件。 |

### [](#移动或拷贝 "移动或拷贝")移动或拷贝

| 函数名 | 描述 |
| --- | --- |
| copy | 拷贝文件 |
| move_uploaded_file | 将上传的文件移动到新位置 |

### [](#读写 "读写")读写

| 函数名 | 描述 |
| --- | --- |
| feof | 测试文件指针是否到了文件结束的位置 |
| fgetc | 从文件指针中读取, 返回一个包含有一个字符的字符串 |
| fgetcsv | 从文件指针中读入一行并解析 `CSV` 字段 |
| fputcsv | 将行格式化为 `CSV` 并写入文件指针 |
| fgets | 从文件指针中读取一行 |
| fgetss | 从文件指针中读取一行并过滤掉 `HTML` 标记 |
| file | 把整个文件读入一个数组中。数组中的每个单元都是文件中相应的一行，包括换行符在内。 |
| readfile | 读入一个文件并写入到输出缓冲。 |
| fscanf | 根据指定的格式对来自打开的文件的输入进行解析。 |
|  |  |
| fread | 读取文件（可安全用于二进制文件） |
| fwrite | 写入文件（可安全用于二进制文件） |
| fputs | `fwrite` 的别名 |
|  |  |
| file_get_contents | 将整个文件读入一个字符串 |
| file_put_contents | 将一个字符串写入文件 |
|  |  |
| parse_ini_file | 解析一个配置文件 |
| parse_ini_string | Parse a configuration string |
|  |  |
| fnmatch | 根据指定的模式来匹配文件名或字符串 |
| glob | 返回匹配指定模式的文件名或目录 |
|  |  |
| fopen | 打开文件或者 `URL` |
| fclose | 关闭一个已打开的文件指针 |
| rewind | 倒回文件指针的位置 |
| fseek | 在文件指针中定位 |
| ftell | 返回文件指针读 / 写的位置 |
|  |  |
| fpassthru | 将给定的文件指针从当前的位置读取到 `EOF`，并把结果写到输出缓冲区。 |
| set_file_buffer | 设置打开文件的缓冲大小。 |
| fflush | 将缓冲内容输出到文件 |
| clearstatcache | 清除文件状态缓存 |

### [](#删除-1 "删除")删除

| 函数名 | 描述 |
| --- | --- |
| unlink | 删除文件 |
| rmdir | 删除目录 |
| delete | 参见 `unlink` 或 `unset` |

### [](#判断 "判断")判断

| 函数名 | 描述 |
| --- | --- |
| is_dir | 判断给定文件名是否是一个目录 |
| is_executable | 判断给定文件名是否可执行 |
| is_file | 判断给定文件名是否为一个正常的文件 |
| is_link | 判断给定文件名是否为一个符号连接 |
| is_readable | 判断给定文件名是否可读 |
| is_uploaded_file | 判断文件是否是通过 `HTTP POST` 上传的 |
| is_writable | 判断给定的文件名是否可写 |
| is_writeable | `is_writable` 的别名 |
| file_exists | 检查文件或目录是否存在 |

### [](#连接Link "连接Link")连接 Link

| 函数名 | 描述 |
| --- | --- |
| link | 建立一个硬连接 |
| linkinfo | 获取一个连接的信息 |
| lstat | 给出一个文件或符号连接的信息 |
| readlink | 返回符号连接指向的目标 |
| symlink | 建立符号连接 |
| lchgrp | Changes group ownership of symlink |
| lchown | Changes user ownership of symlink |

### [](#进程 "进程")进程

| 函数名 | 描述 |
| --- | --- |
| pclose | 关闭进程文件指针 |
| popen | 打开进程文件指针 |

## [](#ErrorHandling "ErrorHandling")ErrorHandling

### [](#创建-1 "创建")创建

| 函数名 | 描述 |
| --- | --- |
| trigger_error | 创建用户定义的错误消息，用于在用户指定的条件下触发一个错误消息。它与内建的错误处理器一同使用，也可以与由 `set_error_handler()` 函数创建的用户自定义函数使用 |
| user_error | `trigger_error` 的别名 |
|  |  |
| set_error_handler | 设置用户自定义的错误处理函数，替换内建的错误处理器 |
| set_exception_handler | 设置用户自定义的异常处理函数，替换内建的异常处理器 |

### [](#获取 "获取")获取

| 函数名 | 描述 |
| --- | --- |
| error_get_last | 以数组的形式返回最后发生的错误 |
| debug_backtrace | 返回异常追溯数组（`backtrace`） |

### [](#清理 "清理")清理

| 函数名 | 描述 |
| --- | --- |
| error_clear_last | 清除内存中最近的异常信息 |

### [](#恢复 "恢复")恢复

| 函数名 | 描述 |
| --- | --- |
| restore_error_handler | 之前的错误处理程序可能是在错误处理程序或用户自定义函数中构建的，恢复内建的错误处理程序 |
| restore_exception_handler | 之前的异常处理程序可能是在异常处理程序或用户自定义函数中构建的，恢复内建的异常处理程序 |

### [](#输出-1 "输出")输出

| 函数名 | 描述 |
| --- | --- |
| error_log | 向服务器错误记录、文件或远程目标发送一个错误 |
| debug_print_backtrace | 输出异常追溯数组（`backtrace`） |

### [](#配置 "配置")配置

| 函数名 | 描述 |
| --- | --- |
| error_reporting | 设置 `PHP` 的报错级别并返回当前级别 |

## [](#Date-Time "Date/Time")Date/Time

### [](#设置时间（时间戳） "设置时间（时间戳）")设置时间（时间戳）

| 函数名 | 描述 |
| --- | --- |
| date_timestamp_set | 设置基于 `Unix` 时间戳的日期和时间 |

### [](#获取时间（时间戳） "获取时间（时间戳）")获取时间（时间戳）

| 函数名 | 描述 |
| --- | --- |
| time | 返回当前时间的 `Unix` 时间戳 |
| microtime | 返回当前 `Unix` 时间戳和微秒数 |
| mktime | 返回一个日期的 `Unix` 时间戳 |
| gmmktime | 返回 `GMT` 日期的 `UNIX` 时间戳 |
| date_timestamp_get | 返回今天的日期和时间的 `Unix` 时间戳 |
| strtotime | 将任何英文文本的日期或时间描述解析为 `Unix` 时间戳 |

### [](#设置时间（非时间戳） "设置时间（非时间戳）")设置时间（非时间戳）

| 函数名 | 描述 |
| --- | --- |
| date_time_set | 用于设置时间 |
| date_date_set | 设置一个新的日期 |
| strftime | 根据区域设置格式化本地日期和时间 |
| gmstrftime | 根据区域设置格式化 `GMT`/`UTC` 日期和时间 |
| date_isodate_set | 根据 `ISO 8601` 标准设置日期，使用周和天的偏移量（而不是使用一个规定的日期） |

### [](#获取时间（非时间戳） "获取时间（非时间戳）")获取时间（非时间戳）

| 函数名 | 描述 |
| --- | --- |
| localtime | 返回本地时间（一个数组存放关于时间的各项信息） |
| getdate | 返回一个根据 `timestamp` 得出的包含有日期信息的结合数组。如果没有给出时间戳，则认为是当前本地时间 |
| gettimeofday | 返回一个包含当前时间信息的数组 |
| strptime | 解析由 `strftime()` 生成的时间 / 日期 |
| date_parse | 返回一个包含指定日的详细信息的关联数组 |
| date_parse_from_format | 根据指定的格式返回一个包含指定日期信息的关联数组 |
|  |  |
| date | 格式化一个本地时间／日期 |
| gmdate | 格式化 `GMT`/`UTC` 日期和时间，并返回格式化的日期字符串 |
| idate | 将本地时间 / 日期格式化为整数，与 `date()` 不同，`idate()` 只接受一个字符作为 `format` 参数 |
| date_format | 返回一个根据指定格式进行格式化的日期 |
| date_interval_format | 用于格式化时间间隔 |
| date_interval_create_from_date_string | Sets up a DateInterval from the relative parts of the string |
|  |  |
| date_sun_info | 返回一个包含有关指定日期与地点的日出 / 日落和黄昏开始 / 黄昏结束的信息的数组 |
| date_sunrise | 返回指定日期与地点的日出时间 |
| date_sunset | 返回指定日期与地点的日落时间 |
|  |  |
| date_create | 返回一个新的 `DateTime` 对象 |
| date_create_from_format | 返回一个根据指定格式进行格式化的新的 `DateTime` 对象 |
| date_create_immutable | Returns new DateTimeImmutable object |
| date_create_immutable_from_format | Returns new DateTime Immutable object formatted according to the specified format |

### [](#时间加减 "时间加减")时间加减

| 函数名 | 描述 |
| --- | --- |
| date_add | 添加日、月、年、时、分和秒到一个日期 |
| date_sub | 从指定日期减去日、月、年、时、分和秒 |
| date_modify | 修改时间戳 |
|  |  |
| date_diff | 返回两个 `DateTime` 对象间的差值 |

### [](#校验 "校验")校验

| 函数名 | 描述 |
| --- | --- |
| checkdate | 用于验证格利高里日期 |

### [](#时区 "时区")时区

| 函数名 | 描述 |
| --- | --- |
| timezone_open | 创建一个新的 `DateTimeZone` 对象 |
| timezone_name_get | 返回时区的名称 |
| timezone_name_from_abbr | 根据时区缩略语返回时区名称 |
| timezone_abbreviations_list | 返回包含夏令时、偏移量和时区名称的关联数组 |
| timezone_identifiers_list | 返回带有所有时区标识符的数值数组 |
| timezone_location_get | 返回指定时区的位置信息 |
| date_offset_get | 返回时区偏移 |
| timezone_offset_get | 返回相对于 `GMT` 的时区偏移 |
| timezone_transitions_get | 返回所有时区转换 |
| timezone_version_get | 以字符串形式返回时区数据库的版本 |
| date_timezone_get | Alias of DateTime::getTimezone |
| date_timezone_set | Alias of DateTime::setTimezone |
| date_default_timezone_get | 返回脚本中所有日期 / 时间函数使用的默认时区 |
| date_default_timezone_set | 设置脚本中所有日期 / 时间函数使用的默认时区 |

### [](#其它 "其它")其它

| 函数名 | 描述 |
| --- | --- |
| date_get_last_errors | 返回解析日期字符串时找到的警告 / 错误 |

## [](#Calendar "Calendar")Calendar

### [](#日历信息、月、星期、时间戳 "日历信息、月、星期、时间戳")日历信息、月、星期、时间戳

| 函数名 | 描述 |
| --- | --- |
| cal_info | 返回选定历法的信息 |
| cal_days_in_month | 返回某个历法中某年中某月的天数 |
|  |  |
| JDDayOfWeek | 返回星期的日期 |
| JDMonthName | 返回月份的名称 |
|  |  |
| jdtounix | 转变`Julian Day`计数为一个`Unix`时间戳 |
| unixtojd | 转变`Unix`时间戳为`Julian Day`计数 |

### [](#日历转换 "日历转换")日历转换

| 函数名 | 描述 |
| --- | --- |
| cal_to_jd | 从一个支持的历法转变为 `Julian Day`（儒略历）计数。 |
| cal_from_jd | 转换`Julian Day`计数到一个支持的历法。 |
|  |  |
| FrenchToJD | 从一个`French Republican`历法（法国共和历）的日期得到`Julian Day`计数。 |
| JDToFrench | 转变一个`Julian Day`计数到`French Republican`历法的日期 |
|  |  |
| GregorianToJD | 转变一个`Gregorian`历法（格利高里历法）日期到`Julian Day`计数 |
| JDToGregorian | 转变一个`Julian Day`计数为`Gregorian`历法日期 |
|  |  |
| JewishToJD | 转变一个`Jewish`历法（犹太历法）的日期为一个`Julian Day`计数 |
| jdtojewish | 转换一个`julian`天数为`Jewish`历法的日期 |
|  |  |
| JulianToJD | 转变一个`Julian`历法（儒略历）的日期为`Julian Day`计数 |
| JDToJulian | 转变一个`Julian Day`计数到`Julian`历法的日期 |

### [](#西方特用 "西方特用")西方特用

| 函数名 | 描述 |
| --- | --- |
| easter_date | 得到指定年份的复活节午夜时的 `Unix` 时间戳。 |
| easter_days | 得到指定年份的 3 月 21 日到复活节之间的天数 |
