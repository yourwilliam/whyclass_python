# python正则表达式

在编程中使用字符串操作的场景非常多，基本的python提供字符串处理方法包括

```python
print(dir(str))

[..........'capitalize', 'casefold', 'center', 'count', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isdecimal', 'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']
```

可以在devdocs或者dash查询每个方法的具体使用情况，使用较多的包含

* `format` 格式化字符串使用
* `isalnum` 判断是否仅由字母和数字组成
* `isalpha` 判断是否仅由字母组成
* `isdecimal` 判断是否仅由数字组成
* `isspace` 判断是否仅由空格组成
* `replace` 部分字符串的替换
* `split` 分割字符串
* `strip` 去掉空格或者其他字符串

可以使用这些函数对字符串进行一系列的操作，来得到我们想要的字符串变化的结果。

如果需要对字符串做更复杂的一些匹配或者替换操作，我们可以使用正则表达式来更方便的执行。

## 正则表达式

> 正则表达式（英语：Regular Expression，在代码中常简写为regex、regexp或RE），又称正規表示式、正規表示法、規則運算式、常規表示法，是计算机科学的一个概念。正则表达式使用单个字符串来描述、匹配一系列符合某个句法规则的字符串。在很多文本编辑器裡，正則表达式通常被用来检索、替换那些符合某个模式的文本。 [wikipedia](https://zh.wikipedia.org/wiki/%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F)

## 正则表达式基本语法

特殊字符是：

*   `.`

    (点) 在默认模式，匹配除了换行的任意字符。如果指定了标签 [`DOTALL`](https://docs.python.org/zh-cn/3/library/re.html#re.DOTALL) ，它将匹配包括换行符的任意字符。
*   `^`

    (插入符号) 匹配字符串的开头， 并且在 [`MULTILINE`](https://docs.python.org/zh-cn/3/library/re.html#re.MULTILINE) 模式也匹配换行后的首个符号。
*   `$`

    匹配字符串尾或者换行符的前一个字符，在 [`MULTILINE`](https://docs.python.org/zh-cn/3/library/re.html#re.MULTILINE) 模式匹配换行符的前一个字符。 `foo` 匹配 `'foo'` 和 `'foobar'` , 但正则 `foo$` 只匹配 `'foo'`。更有趣的是， 在 `'foo1\nfoo2\n'` 搜索 `foo.$` ，通常匹配 `'foo2'` ，但在 [`MULTILINE`](https://docs.python.org/zh-cn/3/library/re.html#re.MULTILINE) 模式 ，可以匹配到 `'foo1'` ；在 `'foo\n'` 搜索 `$` 会找到两个空串：一个在换行前，一个在字符串最后。
*   `*`

    对它前面的正则式匹配0到任意次重复， 尽量多的匹配字符串。 `ab*` 会匹配 `'a'`， `'ab'`， 或者 `'a'``后面跟随任意个 ``'b'`。
*   `+`

    对它前面的正则式匹配1到任意次重复。 `ab+` 会匹配 `'a'` 后面跟随1个以上到任意个 `'b'`，它不会匹配 `'a'`。
*   `?`

    对它前面的正则式匹配0到1次重复。 `ab?` 会匹配 `'a'` 或者 `'ab'`。
*   `*?`, `+?`, `??`

    `'*'`, `'+'`，和 `'?'` 修饰符都是 _贪婪的_；它们在字符串进行尽可能多的匹配。有时候并不需要这种行为。如果正则式 `<.*>` 希望找到 `'<a> b <c>'`，它将会匹配整个字符串，而不仅是 `'<a>'`。在修饰符之后添加 `?` 将使样式以 _非贪婪`方式或者 :dfn:`最小_ 方式进行匹配； 尽量 _少_ 的字符将会被匹配。 使用正则式 `<.*?>` 将会仅仅匹配 `'<a>'`。
*   "{m}"

    对其之前的正则式指定匹配 _m_ 个重复；少于 _m_ 的话就会导致匹配失败。比如， `a{6}` 将匹配6个 `'a'` , 但是不能是5个。
*   "{m, n}"

    对正则式进行 _m_ 到 _n_ 次匹配，在 _m_ 和 _n_ 之间取尽量多。 比如，`a{3,5}` 将匹配 3 到 5个 `'a'`。忽略 _m_ 意为指定下界为0，忽略 _n_ 指定上界为无限次。 比如 `a{4,}b` 将匹配 `'aaaab'` 或者1000个 `'a'` 尾随一个 `'b'`，但不能匹配 `'aaab'`。逗号不能省略，否则无法辨别修饰符应该忽略哪个边界。
*   `{m,n}?`

    前一个修饰符的非贪婪模式，只匹配尽量少的字符次数。比如，对于 `'aaaaaa'`， `a{3,5}` 匹配 5个 `'a'` ，而 `a{3,5}?` 只匹配3个 `'a'`。
*   `\`

    转义特殊字符（允许你匹配 `'*'`, `'?'`, 或者此类其他），或者表示一个特殊序列；特殊序列之后进行讨论。如果你没有使用原始字符串（ `r'raw'` ）来表达样式，要牢记Python也使用反斜杠作为转义序列；如果转义序列不被Python的分析器识别，反斜杠和字符才能出现在字符串中。如果Python可以识别这个序列，那么反斜杠就应该重复两次。这将导致理解障碍，所以高度推荐，就算是最简单的表达式，也要使用原始字符串。
*   `[]`

    用于表示一个字符集合。在一个集合中：字符可以单独列出，比如 `[amk]` 匹配 `'a'`， `'m'`， 或者 `'k'`。可以表示字符范围，通过用 `'-'` 将两个字符连起来。比如 `[a-z]` 将匹配任何小写ASCII字符， `[0-5][0-9]` 将匹配从 `00` 到 `59` 的两位数字， `[0-9A-Fa-f]` 将匹配任何十六进制数位。 如果 `-` 进行了转义 （比如 `[a\-z]`）或者它的位置在首位或者末尾（如 `[-a]` 或 `[a-]`），它就只表示普通字符 `'-'`。特殊字符在集合中，失去它的特殊含义。比如 `[(+*)]` 只会匹配这几个文法字符 `'('`, `'+'`, `'*'`, or `')'`。字符类如 `\w` 或者 `\S` (如下定义) 在集合内可以接受，它们可以匹配的字符由 [`ASCII`](https://docs.python.org/zh-cn/3/library/re.html#re.ASCII) 或者 [`LOCALE`](https://docs.python.org/zh-cn/3/library/re.html#re.LOCALE) 模式决定。不在集合范围内的字符可以通过 _取反_ 来进行匹配。如果集合首字符是 `'^'` ，所有 _不_ 在集合内的字符将会被匹配，比如 `[^5]` 将匹配所有字符，除了 `'5'`， `[^^]` 将匹配所有字符，除了 `'^'`. `^` 如果不在集合首位，就没有特殊含义。在集合内要匹配一个字符 `']'`，有两种方法，要么就在它之前加上反斜杠，要么就把它放到集合首位。比如， `[()[\]{}]` 和 `[]()[{}]` 都可以匹配括号。[Unicode Technical Standard #18](https://unicode.org/reports/tr18/) 里的嵌套集合和集合操作支持可能在未来添加。这将会改变语法，所以为了帮助这个改变，一个 [`FutureWarning`](https://docs.python.org/zh-cn/3/library/exceptions.html#FutureWarning) 将会在有多义的情况里被 `raise`，包含以下几种情况，集合由 `'['` 开始，或者包含下列字符序列 `'--'`, `'&&'`, `'~~'`, 和 `'||'`。为了避免警告，需要将它们用反斜杠转义。_在 3.7 版更改:_ 如果一个字符串构建的语义在未来会改变的话，一个 [`FutureWarning`](https://docs.python.org/zh-cn/3/library/exceptions.html#FutureWarning) 会 `raise` 。
*   `|`

    `A|B`， _A_ 和 _B_ 可以是任意正则表达式，创建一个正则表达式，匹配 _A_ 或者 _B_. 任意个正则表达式可以用 `'|'` 连接。它也可以在组合（见下列）内使用。扫描目标字符串时， `'|'` 分隔开的正则样式从左到右进行匹配。当一个样式完全匹配时，这个分支就被接受。意思就是，一旦 _A_ 匹配成功， _B_ 就不再进行匹配，即便它能产生一个更好的匹配。或者说，`'|'` 操作符绝不贪婪。 如果要匹配 `'|'` 字符，使用 `\|`， 或者把它包含在字符集里，比如 `[|]`.
*   `(...)`

    （组合），匹配括号内的任意正则表达式，并标识出组合的开始和结尾。匹配完成后，组合的内容可以被获取，并可以在之后用 `\number` 转义序列进行再次匹配，之后进行详细说明。要匹配字符 `'('` 或者 `')'`, 用 `\(` 或 `\)`, 或者把它们包含在字符集合里: `[(]`, `[)]`.

由 `'\'` 和一个字符组成的特殊序列在以下列出。 如果普通字符不是ASCII数位或者ASCII字母，那么正则样式将匹配第二个字符。比如，`\$` 匹配字符 `'$'`.

*   `\number`

    匹配数字代表的组合。每个括号是一个组合，组合从1开始编号。比如 `(.+) \1` 匹配 `'the the'` 或者 `'55 55'`, 但不会匹配 `'thethe'` (注意组合后面的空格)。这个特殊序列只能用于匹配前面99个组合。如果 _number_ 的第一个数位是0， 或者 _number_ 是三个八进制数，它将不会被看作是一个组合，而是八进制的数字值。在 `'['` 和 `']'` 字符集合内，任何数字转义都被看作是字符。
*   `\A`

    只匹配字符串开始。
*   `\b`

    匹配空字符串，但只在单词开始或结尾的位置。一个单词被定义为一个单词字符的序列。注意，通常 `\b` 定义为 `\w` 和 `\W` 字符之间，或者 `\w` 和字符串开始/结尾的边界， 意思就是 `r'\bfoo\b'` 匹配 `'foo'`, `'foo.'`, `'(foo)'`, `'bar foo baz'` 但不匹配 `'foobar'` 或者 `'foo3'`。默认情况下，Unicode字母和数字是在Unicode样式中使用的，但是可以用 [`ASCII`](https://docs.python.org/zh-cn/3/library/re.html#re.ASCII) 标记来更改。如果 [`LOCALE`](https://docs.python.org/zh-cn/3/library/re.html#re.LOCALE) 标记被设置的话，词的边界是由当前语言区域设置决定的，`\b` 表示退格字符，以便与Python字符串文本兼容。
*   `\B`

    匹配空字符串，但 _不_ 能在词的开头或者结尾。意思就是 `r'py\B'` 匹配 `'python'`, `'py3'`, `'py2'`, 但不匹配 `'py'`, `'py.'`, 或者 `'py!'`. `\B` 是 `\b` 的取非，所以Unicode样式的词语是由Unicode字母，数字或下划线构成的，虽然可以用 [`ASCII`](https://docs.python.org/zh-cn/3/library/re.html#re.ASCII) 标志来改变。如果使用了 [`LOCALE`](https://docs.python.org/zh-cn/3/library/re.html#re.LOCALE) 标志，则词的边界由当前语言区域设置。
*   `\d`

    对于 Unicode (str) 样式：匹配任何Unicode十进制数（就是在Unicode字符目录\[Nd]里的字符）。这包括了 `[0-9]` ，和很多其他的数字字符。如果设置了 [`ASCII`](https://docs.python.org/zh-cn/3/library/re.html#re.ASCII) 标志，就只匹配 `[0-9]` 。对于8位(bytes)样式：匹配任何十进制数，就是 `[0-9]`。
*   `\D`

    匹配任何非十进制数字的字符。就是 `\d` 取非。 如果设置了 [`ASCII`](https://docs.python.org/zh-cn/3/library/re.html#re.ASCII) 标志，就相当于 `[^0-9]` 。
*   `\s`

    对于 Unicode (str) 样式：匹配任何Unicode空白字符（包括 `[ \t\n\r\f\v]` ，还有很多其他字符，比如不同语言排版规则约定的不换行空格）。如果 [`ASCII`](https://docs.python.org/zh-cn/3/library/re.html#re.ASCII) 被设置，就只匹配 `[ \t\n\r\f\v]` 。对于8位(bytes)样式：匹配ASCII中的空白字符，就是 `[ \t\n\r\f\v]` 。
*   `\S`

    匹配任何非空白字符。就是 `\s` 取非。如果设置了 [`ASCII`](https://docs.python.org/zh-cn/3/library/re.html#re.ASCII) 标志，就相当于 `[^ \t\n\r\f\v]` 。
*   `\w`

    对于 Unicode (str) 样式：匹配Unicode词语的字符，包含了可以构成词语的绝大部分字符，也包括数字和下划线。如果设置了 [`ASCII`](https://docs.python.org/zh-cn/3/library/re.html#re.ASCII) 标志，就只匹配 `[a-zA-Z0-9_]` 。对于8位(bytes)样式：匹配ASCII字符中的数字和字母和下划线，就是 `[a-zA-Z0-9_]` 。如果设置了 [`LOCALE`](https://docs.python.org/zh-cn/3/library/re.html#re.LOCALE) 标记，就匹配当前语言区域的数字和字母和下划线。
*   `\W`

    匹配任何非词语字符。是 `\w` 取非。如果设置了 [`ASCII`](https://docs.python.org/zh-cn/3/library/re.html#re.ASCII) 标记，就相当于 `[^a-zA-Z0-9_]` 。如果设置了 [`LOCALE`](https://docs.python.org/zh-cn/3/library/re.html#re.LOCALE) 标志，就匹配当前语言区域的 _非_ 词语字符。
*   `\Z`

    只匹配字符串尾。

绝大部分Python的标准转义字符也被正则表达式分析器支持。:

```
\a      \b      \f      \n
\r      \t      \u      \U
\v      \x      \\
```

（注意 `\b` 被用于表示词语的边界，它只在字符集合内表示退格，比如 `[\b]` 。）

`'\u'` 和 `'\U'` 转义序列只在 Unicode 样式中支持。 在 bytes 算啊看会显示错误。 未知的 ASCII 字符转义序列保留在未来使用，会被当作错误来处理。

八进制转义包含为一个有限形式。如果首位数字是 0， 或者有三个八进制数位，那么就认为它是八进制转义。其他的情况，就看作是组引用。对于字符串文本，八进制转义最多有三个数位长。

_在 3.3 版更改:_ 增加了 `'\u'` 和 `'\U'` 转义序列。

_在 3.6 版更改:_ 由 `'\'` 和一个ASCII字符组成的未知转义会被看成错误。

## python正则表达式  re模块

*   `re.``compile`(_pattern_, _flags=0_)

    将正则表达式的样式编译为一个 [正则表达式对象](https://docs.python.org/zh-cn/3/library/re.html#re-objects) （正则对象），可以用于匹配，通过这个对象的方法 [`match()`](https://docs.python.org/zh-cn/3/library/re.html#re.Pattern.match), [`search()`](https://docs.python.org/zh-cn/3/library/re.html#re.Pattern.search) 以及其他如下描述。这个表达式的行为可以通过指定 _标记_ 的值来改变。值可以是以下任意变量，可以通过位的OR操作来结合（ `|` 操作符）。序列`prog = re.compile(pattern) result = prog.match(string)`等价于`result = re.match(pattern, string)`如果需要多次使用这个正则表达式的话，使用 [`re.compile()`](https://docs.python.org/zh-cn/3/library/re.html#re.compile) 和保存这个正则对象以便复用，可以让程序更加高效。注解 通过 [`re.compile()`](https://docs.python.org/zh-cn/3/library/re.html#re.compile) 编译后的样式，和模块级的函数会被缓存， 所以少数的正则表达式使用无需考虑编译的问题。
*   `re.``search`(_pattern_, _string_, _flags=0_)

    扫描整个 _字符串_ 找到匹配样式的第一个位置，并返回一个相应的 [匹配对象](https://docs.python.org/zh-cn/3/library/re.html#match-objects)。如果没有匹配，就返回一个 `None` ； 注意这和找到一个零长度匹配是不同的。
*   `re.``match`(_pattern_, _string_, _flags=0_)

    如果 _string_ 开始的0或者多个字符匹配到了正则表达式样式，就返回一个相应的 [匹配对象](https://docs.python.org/zh-cn/3/library/re.html#match-objects) 。 如果没有匹配，就返回 `None` ；注意它跟零长度匹配是不同的。注意即便是 [`MULTILINE`](https://docs.python.org/zh-cn/3/library/re.html#re.MULTILINE) 多行模式， [`re.match()`](https://docs.python.org/zh-cn/3/library/re.html#re.match) 也只匹配字符串的开始位置，而不匹配每行开始。如果你想定位 _string_ 的任何位置，使用 [`search()`](https://docs.python.org/zh-cn/3/library/re.html#re.search) 来替代（也可参考 [search() vs. match()](https://docs.python.org/zh-cn/3/library/re.html#search-vs-match) ）
*   `re.``fullmatch`(_pattern_, _string_, _flags=0_)

    如果整个 _string_ 匹配到正则表达式样式，就返回一个相应的 [匹配对象](https://docs.python.org/zh-cn/3/library/re.html#match-objects) 。 否则就返回一个 `None` ；注意这跟零长度匹配是不同的。_3.4 新版功能._
*   `re.``split`(_pattern_, _string_, _maxsplit=0_, _flags=0_)

    用 _pattern_ 分开 _string_ 。 如果在 _pattern_ 中捕获到括号，那么所有的组里的文字也会包含在列表里。如果 _maxsplit_ 非零， 最多进行 _maxsplit_ 次分隔， 剩下的字符全部返回到列表的最后一个元素。>>>`>>> re.split(r'\W+', 'Words, words, words.') ['Words', 'words', 'words', ''] >>> re.split(r'(\W+)', 'Words, words, words.') ['Words', ', ', 'words', ', ', 'words', '.', ''] >>> re.split(r'\W+', 'Words, words, words.', 1) ['Words', 'words, words.'] >>> re.split('[a-f]+', '0a3B9', flags=re.IGNORECASE) ['0', '3', '9']`如果分隔符里有捕获组合，并且匹配到字符串的开始，那么结果将会以一个空字符串开始。对于结尾也是一样>>>`>>> re.split(r'(\W+)', '...words, words...') ['', '...', 'words', ', ', 'words', '...', '']`这样的话，分隔组将会出现在结果列表中同样的位置。样式的空匹配将分开字符串，但只在不相临的状况生效。`>>> re.split(r'\b', 'Words, words, words.') ['', 'Words', ', ', 'words', ', ', 'words', '.'] >>> re.split(r'\W*', '...words...') ['', '', 'w', 'o', 'r', 'd', 's', '', ''] >>> re.split(r'(\W*)', '...words...') ['', '...', '', '', 'w', '', 'o', '', 'r', '', 'd', '', 's', '...', '', '', '']`_在 3.1 版更改:_ 增加了可选标记参数。_在 3.7 版更改:_ 增加了空字符串的样式分隔。
*   `re.``findall`(_pattern_, _string_, _flags=0_)

    对 _string_ 返回一个不重复的 _pattern_ 的匹配列表， _string_ 从左到右进行扫描，匹配按找到的顺序返回。如果样式里存在一到多个组，就返回一个组合列表；就是一个元组的列表（如果样式里有超过一个组合的话）。空匹配也会包含在结果里。_在 3.7 版更改:_ 非空匹配现在可以在前一个空匹配之后出现了。
*   `re.``finditer`(_pattern_, _string_, _flags=0_)

    _pattern_ 在 _string_ 里所有的非重复匹配，返回为一个迭代器 [iterator](https://docs.python.org/zh-cn/3/glossary.html#term-iterator) 保存了 [匹配对象](https://docs.python.org/zh-cn/3/library/re.html#match-objects) 。 _string_ 从左到右扫描，匹配按顺序排列。空匹配也包含在结果里。_在 3.7 版更改:_ 非空匹配现在可以在前一个空匹配之后出现了。
*   `re.``sub`(_pattern_, _repl_, _string_, _count=0_, _flags=0_)

    返回通过使用 _repl_ 替换在 _string_ 最左边非重叠出现的 _pattern_ 而获得的字符串。 如果样式没有找到，则不加改变地返回 _string_。 _repl_ 可以是字符串或函数；如为字符串，则其中任何反斜杠转义序列都会被处理。 也就是说，`\n` 会被转换为一个换行符，`\r` 会被转换为一个回车附，依此类推。 未知的 ASCII 字符转义序列保留在未来使用，会被当作错误来处理。 其他未知转义序列例如 `\&` 会保持原样。 向后引用像是 `\6` 会用样式中第 6 组所匹配到的子字符串来替换。 例如:>>>`>>> re.sub(r'def\s+([a-zA-Z_][a-zA-Z_0-9]*)\s*\(\s*\):', ... r'static PyObject*\npy_\1(void)\n{', ... 'def myfunc():') 'static PyObject*\npy_myfunc(void)\n{'`如果 _repl_ 是一个函数，那它会对每个非重复的 _pattern_ 的情况调用。这个函数只能有一个 [匹配对象](https://docs.python.org/zh-cn/3/library/re.html#match-objects) 参数，并返回一个替换后的字符串。比如>>>`>>> def dashrepl(matchobj): ... if matchobj.group(0) == '-': return ' ' ... else: return '-' >>> re.sub('-{1,2}', dashrepl, 'pro----gram-files') 'pro--gram files' >>> re.sub(r'\sAND\s', ' & ', 'Baked Beans And Spam', flags=re.IGNORECASE) 'Baked Beans & Spam'`样式可以是一个字符串或者一个 [样式对象](https://docs.python.org/zh-cn/3/library/re.html#re-objects) 。可选参数 _count_ 是要替换的最大次数；_count_ 必须是非负整数。如果忽略这个参数，或者设置为0，所有的匹配都会被替换。空匹配只在不相临连续的情况被更替，所以 `sub('x*', '-', 'abxd')` 返回 `'-a-b--d-'` 。在字符串类型的 _repl_ 参数里，如上所述的转义和向后引用中，`\g<name>` 会使用命名组合 `name`，（在 `(?P<name>…)` 语法中定义） `\g<number>` 会使用数字组；`\g<2>` 就是 `\2`，但它避免了二义性，如 `\g<2>0`。 `\20` 就会被解释为组20，而不是组2后面跟随一个字符 `'0'`。向后引用 `\g<0>` 把 _pattern_ 作为一整个组进行引用。_在 3.1 版更改:_ 增加了可选标记参数。_在 3.5 版更改:_ 不匹配的组合替换为空字符串。_在 3.6 版更改:_ _pattern_ 中的未知转义（由 `'\'` 和一个 ASCII 字符组成）被视为错误。_在 3.7 版更改:_ _repl_ 中的未知转义（由 `'\'` 和一个 ASCII 字符组成）被视为错误。_在 3.7 版更改:_ 样式中的空匹配相邻接时会被替换。
*   `re.``subn`(_pattern_, _repl_, _string_, _count=0_, _flags=0_)

    行为与 [`sub()`](https://docs.python.org/zh-cn/3/library/re.html#re.sub) 相同，但是返回一个元组 `(字符串, 替换次数)`._在 3.1 版更改:_ 增加了可选标记参数。_在 3.5 版更改:_ 不匹配的组合替换为空字符串。
*   `re.``escape`(_pattern_)

    转义 _pattern_ 中的特殊字符。如果你想对任意可能包含正则表达式元字符的文本字符串进行匹配，它就是有用的。比如>>>`>>> print(re.escape('python.exe')) python\.exe >>> legal_chars = string.ascii_lowercase + string.digits + "!#$%&'*+-.^_`|\~:" >>> print('\[%s]+' % re.escape(legal_chars)) \[abcdefghijklmnopqrstuvwxyz0123456789!#$%\\&'\*+-.\\^_`\|\~:]+ >>> operators = ['+', '-', '*', '/', '**'] >>> print('|'.join(map(re.escape, sorted(operators, reverse=True)))) /|\-|\+|\*\*|\*`这个函数不能用在 [`sub()`](https://docs.python.org/zh-cn/3/library/re.html#re.sub) 和 [`subn()`](https://docs.python.org/zh-cn/3/library/re.html#re.subn) 的替换字符串里，只有反斜杠应该被转义，比如说>>>`>>> digits_re = r'\d+' >>> sample = '/usr/sbin/sendmail - 0 errors, 12 warnings' >>> print(re.sub(digits_re, digits_re.replace('\\', r'\\'), sample)) /usr/sbin/sendmail - \d+ errors, \d+ warnings`_在 3.3 版更改:_ `'_'` 不再被转义。_在 3.7 版更改:_ 只有在正则表达式中可以产生特殊含义的字符会被转义。
*   `re.``purge`()

    清除正则表达式缓存。
*   _exception_ `re.``error`(_msg_, _pattern=None_, _pos=None_)

    `raise` 一个例外。当传递到函数的字符串不是一个有效正则表达式的时候（比如，包含一个不匹配的括号）或者其他错误在编译时或匹配时产生。如果字符串不包含样式匹配，是不会被视为错误的。错误实例有以下附加属性：`msg`未格式化的错误消息。`pattern`正则表达式样式。`pos`编译失败的 _pattern_ 的位置索引（可以是 `None` ）。`lineno`对应 _pos_ (可以是 `None`) 的行号。`colno`对应 _pos_ (可以是 `None`) 的列号。_在 3.5 版更改:_ 添加了附加属性。

    **python正则表达式  正则对象**

    编译后的正则表达式对象支持一下方法和属性：
*   `Pattern.``search`(_string_\[, _pos_\[, _endpos_]])

    扫描整个 _string_ 寻找第一个匹配的位置， 并返回一个相应的 [匹配对象](https://docs.python.org/zh-cn/3/library/re.html#match-objects)。如果没有匹配，就返回 `None` ；注意它和零长度匹配是不同的。可选的第二个参数 _pos_ 给出了字符串中开始搜索的位置索引；默认为 `0`，它不完全等价于字符串切片； `'^'` 样式字符匹配字符串真正的开头，和换行符后面的第一个字符，但不会匹配索引规定开始的位置。可选参数 _endpos_ 限定了字符串搜索的结束；它假定字符串长度到 _endpos_ ， 所以只有从 `pos` 到 `endpos - 1` 的字符会被匹配。如果 _endpos_ 小于 _pos_，就不会有匹配产生；另外，如果 _rx_ 是一个编译后的正则对象， `rx.search(string, 0, 50)` 等价于 `rx.search(string[:50], 0)`。>>>`>>> pattern = re.compile("d") >>> pattern.search("dog") # Match at index 0 <re.Match object; span=(0, 1), match='d'> >>> pattern.search("dog", 1) # No match; search doesn't include the "d"`
*   `Pattern.``match`(_string_\[, _pos_\[, _endpos_]])

    如果 _string_ 的 _开始位置_ 能够找到这个正则样式的任意个匹配，就返回一个相应的 [匹配对象](https://docs.python.org/zh-cn/3/library/re.html#match-objects)。如果不匹配，就返回 `None` ；注意它与零长度匹配是不同的。可选参数 _pos_ 和 _endpos_ 与 [`search()`](https://docs.python.org/zh-cn/3/library/re.html#re.Pattern.search) 含义相同。>>>`>>> pattern = re.compile("o") >>> pattern.match("dog") # No match as "o" is not at the start of "dog". >>> pattern.match("dog", 1) # Match as "o" is the 2nd character of "dog". <re.Match object; span=(1, 2), match='o'>`如果你想定位匹配在 _string_ 中的位置，使用 [`search()`](https://docs.python.org/zh-cn/3/library/re.html#re.Pattern.search) 来替代（另参考 [search() vs. match()](https://docs.python.org/zh-cn/3/library/re.html#search-vs-match)）。
*   `Pattern.``fullmatch`(_string_\[, _pos_\[, _endpos_]])

    如果整个 _string_ 匹配这个正则表达式，就返回一个相应的 [匹配对象](https://docs.python.org/zh-cn/3/library/re.html#match-objects) 。 否则就返回 `None` ； 注意跟零长度匹配是不同的。可选参数 _pos_ 和 _endpos_ 与 [`search()`](https://docs.python.org/zh-cn/3/library/re.html#re.Pattern.search) 含义相同。>>>`>>> pattern = re.compile("o[gh]") >>> pattern.fullmatch("dog") # No match as "o" is not at the start of "dog". >>> pattern.fullmatch("ogre") # No match as not the full string matches. >>> pattern.fullmatch("doggie", 1, 3) # Matches within given limits. <re.Match object; span=(1, 3), match='og'>`_3.4 新版功能._
*   `Pattern.``split`(_string_, _maxsplit=0_)

    等价于 [`split()`](https://docs.python.org/zh-cn/3/library/re.html#re.split) 函数，使用了编译后的样式。
*   `Pattern.``findall`(_string_\[, _pos_\[, _endpos_]])

    类似函数 [`findall()`](https://docs.python.org/zh-cn/3/library/re.html#re.findall) ， 使用了编译后样式，但也可以接收可选参数 _pos_ 和 _endpos_ ，限制搜索范围，就像 [`search()`](https://docs.python.org/zh-cn/3/library/re.html#re.search)。
*   `Pattern.``finditer`(_string_\[, _pos_\[, _endpos_]])

    类似函数 `finiter()` ， 使用了编译后样式，但也可以接收可选参数 _pos_ 和 _endpos_ ，限制搜索范围，就像 [`search()`](https://docs.python.org/zh-cn/3/library/re.html#re.search)。
*   `Pattern.``sub`(_repl_, _string_, _count=0_)

    等价于 [`sub()`](https://docs.python.org/zh-cn/3/library/re.html#re.sub) 函数，使用了编译后的样式。
*   `Pattern.``subn`(_repl_, _string_, _count=0_)

    等价于 [`subn()`](https://docs.python.org/zh-cn/3/library/re.html#re.subn) 函数，使用了编译后的样式。
*   `Pattern.``flags`

    正则匹配标记。这是可以传递给 [`compile()`](https://docs.python.org/zh-cn/3/library/re.html#re.compile) 的参数，任何 `(?…)` 内联标记，隐性标记比如 `UNICODE` 的结合。
*   `Pattern.``groups`

    捕获组合的数量。
*   `Pattern.``groupindex`

    映射由 `(?P<id>)` 定义的命名符号组合和数字组合的字典。如果没有符号组，那字典就是空的。
*   `Pattern.``pattern`

    编译对象的原始样式字符串。

_在 3.7 版更改:_ 添加 [`copy.copy()`](https://docs.python.org/zh-cn/3/library/copy.html#copy.copy) 和 [`copy.deepcopy()`](https://docs.python.org/zh-cn/3/library/copy.html#copy.deepcopy) 函数的支持。编译后的正则表达式对象被认为是原子性的。
