# Talk-More-About-FrontEnd

Talk more about FrontEnd in one full path.

## 编程语言通识

非形式语言：中文，英文
形式语言（乔姆斯基谱系）：
0 型 无限制文法
1 型 上下文相关文法
2 型 上下文无关文法
3 型 正则文法 限制表达能力

现代语言会采取折中的办法，将语言分为词法和语法两个部分。将语言变为单个的词，在把这些词变为输入流做为语法分析。因此现在的主流语言分为词法和语法两个部分。

#### 产生式(BNF)

BNF 范式是一种用递归的思想来表述计算机语言符号集的定义规范
法则：
::=表示定义；
“ ”双引号里的内容表示字符；
<>尖括号里的内容表示必选内容；
| 竖线两边的是可选内容，相当于 or；
作者：不是 Zoe
链接：https://www.zhihu.com/question/27051306/answer/579820547
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

BNF 是 John Backus 在 20 世纪 90 年代提出的用以简洁描述一种编程语言的语言。
基本结构为：`<non-terminal> ::= <replacement>`
non-terminal 意为非终止符，就是说我们还没有定义完的东西，还可以继续由右边的 replacement，也就是代替物来进一步解释、定义。
举个例子：在中文语法里，一个句子一般由“主语”、“谓语”和“宾语”组成，主语可以是名词或者代词，谓语一般是动词，宾语可以使形容词，名词或者代词。那么“主语”、“谓语”和“宾语”就是非终止符，因为还可以继续由“名词”、“代词”、“动词”、“形容词”等替代。
例 1. <句子> ::= <主语><谓语><宾语>
例 2. <主语> ::= <名词> | <代词>
例 3. <谓语>::= <动词>
例 4. <宾语>::= <形容词> | <名词> | <代词>
例 5. <代词>::= <我>
例 6. <动词>::= <吃>
例 7. <动词>::= <喜欢>
例 8. <名词>::= <车>
例 9. <名词>::= <肉>
如上，在 ::= 左边的就是 non-terminal 非终止符，右边的就是 replacement，可以是一系列的非终止符，如例 1 中的 replacement 便是后面例 234 左边的非终止符，也可以是终止符，如例 56789 的右边，找不到别的符号来进一步代替。因此，终止符永远不会出现在左边。一旦我们看到了终止符，这个描述过程就结束了。

例 1：定义递归的程序以及十进制数字，或者带有递归的加法运算

```
"a"
"b"
<Program>:= "a"+ | "b"+
<Program>:= <Program> "a"+ | <Program>"b"+

<Number> = "0" | "1" | "2" | .... | "9"
<DecimalNumber> = "0" | ( ("1" | "2" | .... | "9") <Number>*)
<Expression> = <DecimalNumber> "+" <DecimalNumber>
<Expression> = <Expression> "+" <DecimalNumber>

```

例 2： 四则运算 1 + 2 _ 3
终结符 Number
+-_/
非终结符
MultiplicativeExpression
AdditiveExpression

```
<Number> = "0" | "1" | "2" | .... | "9"
<DecimalNumber> = "0" | ( ("1" | "2" | .... | "9") <Number>*)
<DecimalNumber> = /0|[1-9][0-9]*/ 正则表达
<AdditiveExpression> ::= <DecimalNumber> | <AdditiveExpression> "+" <DecimalNumber>
<MultiplicativeExpression> ::= <DecimalNumber> | <MultiplicativeExpression> "*" <DecimalNumber>

<MultiplicativeExpression> ::= <DecimalNumber> |
  <MultiplicativeExpression> "*" <DecimalNumber> |
  <MultiplicativeExpression> "/" <DecimalNumber>

<AdditiveExpression> ::= <MultiplicativeExpression> |
  <AdditiveExpression> "+" <MultiplicativeExpression> |
  <AdditiveExpression> "-" <MultiplicativeExpression>

<LogicalExpression> ::= <AdditiveExpression> |
  <LogicalExpression> "||" <AdditiveExpression> |
  <LogicalExpression> "&&" <AdditiveExpression>

<PrimaryExpression> ::= <DecimalNumber> |
  "(" <LogicalExpression> ")"

```

通过产生式理解乔姆斯基谱系
0 型 无限制文法 ? ::= ?
1 型 上下文相关文法 ?<A>? ::= ?<B>? 也就是中间的部分可以变化
2 型 上下文无关文法 <A> ::= ? 也就是 A 和右边无关; javascript 主要是 2 型文法
3 型 正则文法 <A> ::= <A>? 左递归

#### 图灵完备性

命令式-图灵机
goto
if 和 while
声明式-lambda
递归

如果一系列操作数据的规则（如指令集、编程语言、细胞自动机）按照一定的顺序可以计算出结果，被称为图灵完备（turing complete。图灵完备的语言，有循环执行语句，判断分支语句等。理论上能解决任何算法。但有可能进入死循环而程序崩溃。

#### 动态和静态

动态语言：
在用户的设备/在线服务器上
产品实时运行时
Runtime

静态语言
在程序员的设备上
产品开发时
Compile time

类型系统
动态类型系统与静态类型系统
强类型和弱类型
String + Number
String == Boolean
复合类型包括:
结构体: 对象就是结构体
函数签名:

```
{
  a: T1
  b: T2
}
(T1, T2) => T3
```

子类型包括:
逆变和协变, 凡是能够用 Array<Parent> 的地方都能使用 Array<Child>;凡是能用 Function<Child> 的地方都能使用 Function<Parent>.

一般命令式编程语言
语法通过语义在运行时运行。

Atom:

- Identifier
- Literal

Expression:

- Atom
- Operator
- Punctuator

Statement:

- Expression
- Keyword
- Punctuator

Structure:

- Function
- Class
- Process
- Namespace

Program:

- Program
- Module
- Package
- Library

#### 对于 JavaScript 我们重点参看 A Grammar Summary':

##### 'Lexical Grammar'

- SourceCharacter ::
  any Unicode code point

关于 unicode 参看：
`http://www.fileformat.info/info/unicode/block/index.htm`

```
for (let i = 0; i < 128; i++) {
  // console.log(String.fromCharCode(i));
  document.write(
    i +
      '<span style="background-color:green">' +
      String.fromCharCode(i) +
      '</span></br>'
  );
}
```

转换 unicode: `"黄".codePointAt(1).toString(16)`

- InputElementDiv ::
  WhiteSpace
  LineTerminator
  Comment
  CommonToken
  DivPunctuator
  RightBracePunctuator

对上面的元素进一步分析得到，

- WhiteSpace ::
  <TAB> `'\t'.codePointAt(0).toString(16)`
  <VT>
  <FF>
  <SP> space 就是空格键
  <NBSP> no-break-space 用来处理排版的，让其中的词不会断开，也可以使用 "\u00A0"
  <ZWNBSP> zero-width-no-break-space "\uFEFF" 但是没法找到，bitordermust
  <USP>

- LineTerminator ::
  <LF> line feed /n 建议使用 /n `'\n'.codePointAt(0).toString(16)` '\u000a'
  <CR> carriage return 回车 /r `'\r'.codePointAt(0).toString(16)` '\u000d'
  <LS> 不建议使用后两个，因为超出了 unicode，
  <PS>

- Comment ::
  MultiLineComment '/\* \*/'
  SingleLineComment '// '

- CommonToken ::
  IdentifierName
  Keywords
  Punctuator
  NumericLiteral
  StringLiteral
  Template

- IdentifierName ::
  IdentifierStart
  IdentifierName IdentifierPart

- Literal
  String
  Number
  Boolean
  Object
  Null
  Undefined
  Symbol

- Number
  DecimalLiteral .toString() parseInt("100", 2)
  BinaryIntegerLiteral
  OctalInterLiteral
  HexIntegerLiteral

一些注意点：
Number.MAX_SAFE_INTEGER.toString(16)
Math.abs(0.1 + 0.2 - 0.3) <= Number.EPSILON
如果想让精确，最好都转化为整数

One of escape sequence

\n '\0x000A'
\b '0x0008'
\r '0x000D'
\t '0x0009'
\" '0x0022'  
\' '0x0027'
\\ '0x005C'
