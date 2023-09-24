---
title: Regular
comments: true
date: 2020-07-20 17:07:08
tags:
categories: JAVA
---



#### Tool Website

https://regex101.com/

https://ihateregex.io/expr/password
https://deerchao.cn/tools/wegester/



#### ASCII

![在这里插入图片描述](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTcwMTE5MTAyNjAxNzA5?x-oss-process=image/format,png)

读ASCII表 先读 “横”座标,后读 “纵” 座标.
例如：A , [二进制](https://so.csdn.net/so/search?q=二进制&spm=1001.2101.3001.7020)是 0100 0001 十进制是 2^6 + 1 = 65 十六进制 41

F : 二进制是 0100 0110 十进制是 2^6 + 2^2+2=70 十六进制 46



##### String中的数字转int

```kotlin
val digits = "23"
val c = digits[0] - '0' // 50 - 48
println(digits[0].code) // ASCII是 50  ,16进制是0x32,可以在表中查出是2
println('0'.code)       //ASCII是 48
```



#### 正则意义对照表格

https://www.jb51.net/shouce/jquery1.82/regexp.html

https://baixin.ink/2016/03/21/regular-expression/

https://www.bilibili.com/video/BV1Eq4y1E79W?p=4

https://deerchao.cn/tutorials/regex/regex.htm


https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions

https://medium.com/factory-mind/regex-tutorial-a-simple-cheatsheet-by-examples-649dc1c3f285

### 语法

#### 字符

##### 普通字符

字母、数字、汉字、下划线、以及没有特殊定义的标点符号都是普通字符。直接匹配与之相同的字符

-简单的转义字符

| \n   | 换行符 |
| ---- | ------ |
| \t   | 制表符 |
| \\   | \本身  |



其他都是类似  \^ \$  \( 这样匹配这些字符本身的（还有    ) { } ? + * | [ ]    ）

##### 标准字符集合

 能够与多种字符匹配的表达式  注意区分大小写 大写是相反的意思

| \d   | 任意一个数字，0-9中任意一个     \D 表示所有非数字            |
| ---- | ------------------------------------------------------------ |
| \w   | 任意一个字母或下划线，也就是A-Z、a-z、0-9、_ 、中的任意一个  |
| \s   | 包括空格、制表符、换行符等空白字符中的任意一个               |
| .    | 小数点可以匹配任意一个字符（除了换行符）。如果要匹配包括“\n”在内的所有字符，一般用 [\s\S] |
| \S   | 匹配任何非**空白**字符。等价于[^ \f\n\r\t\v]。 (注意是空白字符，不是空格) |



##### 自定义字符集合

[]方括号匹配方式 ，能够匹配方括号中任意一个字符。**^符号在方括号里表示 取反  方括号外表示零宽标记**，见后面

| [ab5@]    | 匹配 “a”或“b”或“5”或“@”                |
| --------- | -------------------------------------- |
| [^abc]    | 匹配“a”、“b”、”c“之外的任意一个字符    |
| [f-k]     | 匹配“f”-“k”之间的任意一个字母          |
| [^A-F0-3] | 匹配“A”-“F”，“0”-“3”之外的任意一个字符 |

* 正则表达式的特殊符号，被包含到中括号中则失去其特殊意义（就表示自身这个字符），除了^,-之外。

* 标准字符集合，除小数点外，如果被包含于中括号，自定义字符集合将包含该集合。

  比如： [\d.\-+]将匹配：数字、小数点、+、- 本身意义，除非加转义字符\ 

  

  上面两句一个意思呀

#### 量词Quantifier

修饰匹配次数的特殊符号

| {n}   | 表达式重复n次                     | 如：\d{6}  匹配6位数字  \d\d{6} 匹配7位数字  {\d\d}{6} 匹配12位数字 |
| ----- | --------------------------------- | ------------------------------------------------------------ |
| {m,n} | 表达式至少重复m次，最多重复n次    |                                                              |
| {m,}  | 至少重复m次                       |                                                              |
| ？    | 匹配表达式0次或1次 ，相当于{0，1} | 如：a\d{0,1}b  a\d?b  是等价的                               |
| +     | 表达式至少出现1次,相当于{1，}     | 如：a\d+b                                                    |
| *     | 表达式不出现或出现任意次          | 相当于{0，}                                                  |
| |     | 选其中之一的条件			｜匹配x或y。例如，“z|food”能匹配“z”或“food”。“(z|f)ood”则匹配“zood”或“food”｜

匹配次数中的贪婪模式 （匹配字符数越多越好，默认的）如\d{3,6} 会优先匹配 6位数字

匹配次数中的非贪婪模式 （匹配字符越少越好，修饰匹配次数的特殊符号后再加上一个“？”号）


对于 ` 2[0-4]\d|25[0-5]|[01]?\d\d? ` 的ip地址解析可以这样理解
 2[0-4]\d :  200- 249
 25[0-5]  :  250 - 255
 [01]?\d\d? :  0- 199
 这样就覆盖了所有能填的ip地址。

 ##### {n} 
 o{2}” 
 不能匹配“Bob”中的“o”，因为只有1个o, 但是能匹配“food”中的两个o .

 {n,}	
 n是一个非负整数。至少匹配n次。例如，“o{2,}”不能匹配“Bob”中的“o”，但能匹配“foooood”中的所有o。“o{1,}”等价于“o+”。“o{0,}”则等价于“o*”。

 

#### 字符边界(零宽，不占长度)

-（本组标记匹配的不是字符而是位置，符合某种条件的位置）

| ^    | 匹配输入字符串的开始位置，除非在方括号表达式中使用，当该符号在方括号表达式中使用时，表示不接受该方括号表达式中的字符集合。要匹配 ` ^ ` 字符本身，请使用 ` \^ `。 |
| ---- | ------------------------------------------------------------ |
| $    | 与字符结束的地方匹配                                         |
| \b   | 匹配一个单词边界                                             |

` ^ ` []部分也有描述.

https://www.runoob.com/regexp/regexp-syntax.html



REG : John\b

John 匹配 可以看到 John_	下划线_就是\b的位置，他的左侧n 匹配，但是右侧空格不匹配 \w,所以就是不全是\w,所以匹配。



-\b匹配这样一个位置：前面的字符和后面的字符不全是\w （全是的就不匹配）

如：^i  匹配 i开头的位置    i$ 匹配i结束的位置  hello\b  匹配前后不全是\w表示的hello 

 

#### 匹配模式

IGNORECASE

忽略大小写 默认情况下正则表达式区分大小写(Case Insensitive)

SINGLELINE

单行模式  整个文本看作一个字符串，只有一个开头，一个结尾。使得小数点“.”可以匹配包含换行符（\n）在内的任意字符

MULTILINE

多行模式 每行都是一个字符串，都有开头和结尾。在指定了此模式后，如果需要仅匹配字符串开始和结束位置，可以使用\A和\Z

如：\Ai匹配 第一行第一个i     ^i 匹配每一行第一个的i   i$匹配每一行的最后一个i  i\Z  匹配整个文档最后一个i

 

#### 选择符和分组

| 表达式                  | 作用                                                         |                 |
| ----------------------- | ------------------------------------------------------------ | --------------- |
| \| 分支结构             | 左右两边表达式之间 “或” 关系，匹配左边或者右边               | 表示“或”   如 h |
| ()   捕获组             | (1) 在被修饰匹配次数的时候，括号中的表达式可以作为整体被修饰<br/><br/> (2)取匹配结果的时候，括号中的表达式匹配到的内容可以被单独地编号    <br/><br/> (3)每一对括号会被分配一个编号，使用（）的捕获根据左括号的顺序从1开始自动编号。捕获元素编号为零的第一 个捕获是由整个正则表达式模式匹配的内容 |                 |
| (?:Expression) 非捕获组 | 一些表达式中，不得不使用（），但又不需要保存（）中的子表达式匹配的内容，这时可以用非捕获组来抵消使用（）带来的副作用。节省内存。 |                 |

 


#### 反向引用（\nnn）\nnn表示可以匹配多位数字

-每一对（）会分配一个编号，使用（）的捕获根据左括号的顺序从1开始自动编号。

-通过反向引用，可以对分组已捕获的字符串进行引用。

  如  ([a-z]{2})\1  中的\1 代表第一个组里的内容,匹配到gogo，toto，dodo这样的字符串。

（）（）（） 捕获的内容分别用\1 \2 \3  编号以左括号为准。


#### 后向引用

使用小括号指定一个子表达式后，匹配这个子表达式的文本(也就是此分组捕获的内容)可以在表达式或其它程序中作进一步的处理。默认情况下，每个分组会自动拥有一个组号，规则是：从左向右，以分组的左括号为标志，第一个出现的分组的组号为1，第二个为2，以此类推。

后向引用用于重复搜索前面某个分组匹配的文本。例如，\1代表分组1匹配的文本。难以理解？请看示例：

\b(\w+)\b\s+\1\b可以用来匹配重复的单词，像go go, 或者kitty kitty。这个表达式首先是一个单词，也就是单词开始处和结束处之间的多于一个的字母或数字(\b(\w+)\b)，这个单词会被捕获到编号为1的分组中，然后是1个或几个空白符(\s+)，最后是分组1中捕获的内容（也就是前面匹配的那个单词）(\1)。

上面 \1 就代表 go了， \2的表达式还没搞出来

https://deerchao.cn/tutorials/regex/regex.htm


#### ?

当该字符紧跟在任何一个其他限制符（*,+,?，{n}，{n,}，{n,m}）后面时，匹配模式是非贪婪的。非贪婪模式尽可能少的匹配所搜索的字符串，而默认的贪婪模式则尽可能多的匹配所搜索的字符串。例如，对于字符串“oooo”，“o+?”将匹配单个“o”，而“o+”将匹配所有“o”。



预搜索（零宽断言）（也叫环视）

1. 只进行子表达式的匹配，匹配内容不计入最终的匹配结果，是零宽度,应该可以理解为只匹配，不消耗字符。
2. 这个位置应该符合某个条件。判断当前位置的前后字符，是否符合指定的条件，但不匹配前后的字符。**是对位置的匹配**。
3. 正则表达式匹配过程中，如果子表达式匹配到的是字符内容，而非位置，并被保存到最终的匹配结果中，那么就认为这个子表达式是占有字符的；如果子表达式匹配的仅仅是位置，或者匹配的内容并不保存到最终的匹配结果中，那么就认为这个子表达式是零宽度的。占有字符还是零宽度，是针对匹配的内容是否保存到最终的匹配结果中而言的。

| 表达式   | 作用                                    |
| -------- | --------------------------------------- |
| (?=exp)  | 断言自身出现的位置的后面能匹配表达式exp |
| (?<=exp) | 断言自身出现的位置的前面能匹配表达式exp |
| (?!exp)  | 断言此位置的后面不能匹配表达式exp       |
| (?<!exp) | 断言此位置的前面不能匹配表达式exp       |


##### (?:pattern)	

匹配pattern但不获取匹配结果，也就是说这是一个非获取匹配，不进行存储供以后使用。这在使用或字符“(|)”来组合一个模式的各个部分是很有用。

例如
“industr(?:y|ies|he)”
就是一个比“industry|industries|industrhe”更简略的表达式。

(?:foo){1,2}
如果表达式是 /foo{1,2}/，{1,2} 将只应用于 'foo' 的最后一个字符 'o'，可以看上面的{n}。如果使用非捕获括号，则 {1,2} 会应用于整个 'foo' 单词
![image](https://github.com/noteforme/noteforme.github.io/assets/6995071/9cffc9b1-a7ab-4a0d-912c-80a7691cc0d1)
![image](https://github.com/noteforme/noteforme.github.io/assets/6995071/3c78f534-2dab-4ecf-beb9-63c5f638bbff)
可以看到， foo最多匹配两个，超过的就分组了。


##### (?=exp)
也叫零宽度正预测先行断言，它断言自身出现的位置的后面能匹配表达式exp。比如\b\w+(?=ing\b)，匹配以ing结尾的单词的前面部分(除了ing以外的部分)，
如查找I'm singing while you're dancing.时，它会匹配sing和danc

x(?=y)	需匹配文案x在前面
匹配'x'仅仅当'x'后面跟着'y'.这种叫做先行断言。
例如，/Jack(?=Sprat)/会匹配到'Jack'仅当它后面跟着'Sprat'。/Jack(?=Sprat|Frost)/匹配‘Jack’仅当它后面跟着'Sprat'或者是‘Frost’。但是‘Sprat’和‘Frost’都不是匹配结果的一部分。

正向肯定预查，在任何匹配pattern的字符串开始处匹配查找字符串。
这是一个非获取匹配，也就是说，该匹配不需要获取供以后使用。
例如，“Windows(?=95|98|NT|2000)”能匹配“Windows2000”中的“Windows”，但不能匹配“Windows3.1”中的“Windows”。预查不消耗字符，也就是说，在一个匹配发生后，在最后一次匹配之后立即开始下一次匹配的搜索，而不是从包含预查的字符之后开始。



##### (?!pattern)	
正向否定预查，在任何不匹配pattern的字符串开始处匹配查找字符串。
这是一个非获取匹配，也就是说，该匹配不需要获取供以后使用。例如“Windows(?!95|98|NT|2000)”能匹配“Windows3.1”中的“Windows”，但不能匹配“Windows2000”中的“Windows”。预查不消耗字符，也就是说，在一个匹配发生后，在最后一次匹配之后立即开始下一次匹配的搜索，而不是从包含预查的字符之后开始


##### (?<=pattern)	
反向肯定预查，** 与正向肯定预查类拟，只是方向相反 **。 
例如，“(?<=95|98|NT|2000)Windows”能匹配“2000Windows”中的“Windows”，但不能匹配“3.1Windows”中的“Windows”。

(?<=y)x	
需匹配文案x在后面


##### (?<!pattern)	
反向否定预查，与正向否定预查类拟，只是方向相反。
例如“(?<!95|98|NT|2000)Windows”能匹配“3.1Windows”中的“Windows”，但不能匹配“2000Windows”中的“Windows”。



https://deerchao.cn/tutorials/regex/regex.htm

(?<=\d)[a-z]+

22john



如：[a-z]+(?=ing) 匹配ing结尾的字符串，但不匹配ing本身

       [a-z]+(?=\d+) 匹配数字结尾的字符串    
### 常用的一些正则表达式

##### 电话号码验证

（包含固话和手机号，不能确认号码一定存在，只能匹配格式）

（1）电话号码由数字和“-”构成

（2）电话号码为7-8位

（3）如果电话号码中包含有区号，那么区号为3位或4位，首位是0

（4）区号用“-”和其他部分隔开

（5）移动电话号码为11位

（6）11位移动电话号码的第一位和第二位为“13”“15”“18”

 固话   0\d{2,3}-\d{7,9}   手机号    1[35789]\d{9}

 

##### 电子邮箱地址验证

1.用户名：字母、数字、中划线、下划线组成

2.@

3.网址：字母、数字组成

4.小数点。

5.组织域名：2-4位字母组成

不区分大小写

[\w\-]+@[a-z0-9A-Z]+(\.[A-Za-z]{2,4}){1,2} 

如：ssahdahd@sina.com.cn

##### 常用正则表达式列表 

| 表达式                                        | 功能                              |
| --------------------------------------------- | --------------------------------- |
| [\u4e00-\u9fa5]                               | 匹配中文字符                      |
| \n\s*\r                                       | 匹配空白行                        |
| `<(\S*?)[^>]*>.*?</\1>|<.*? />`               | 断言此位置的后面不能匹配表达式exp |
| `^\s*\s*$`                                    | 匹配首尾空白字符                  |
| `\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*` | 匹配Email地址                     |
| `[a-zA-z]+://[^\s]*`                          | 匹配网址URL                       |
| `\d{3}-\d{8}\d{4}-\d{7}`                      | 匹配国内电话号码                  |
| `[1-9][0-9]{4,}`                              | 匹配腾讯QQ号                      |
| `[1-9]\d{5}(?!\d)`                            | 匹配中国邮政编码                  |
| `\d{15}\d{18}`                                | 匹配身份证                        |
| `\d+\.\d+\.\d+\.\d+`                          | 匹配ip地址                        |



括号

https://www.bilibili.com/video/BV1ef4y1U7V4/?spm_id_from=333.788.recommend_more_video.-1

   

### 工作学习中各种环境的使用

##### JAVA程序中使用正则表达式

相关类位于：**java.util.regex包下面**：

1. **类 Pattern：**
    正则表达式的编译表示形式。
    Pattern p = Pattern.compile(r,int); //建立正则表达式，并启用相应模式
2. **类 Matcher：**
    通过解释 Pattern 对 character sequence 执行匹配操作的引擎。
    Matcher m = p.matcher(str); //匹配str字符串
3. **java代码应用正则的查找、分组、替换、分割：**

##### 查找

```java
package com.bjsxt.regex.test;

import java.util.regex.Matcher;
import java.util.regex.Pattern;

/**
 * 测试正则表达式对象的基本用法
 */
public class RegularTest {
	public static void main(String[] args) {
		//在这个字符串：abcd1234，是否符合指定的正则表达式：\w+
		//表达式对象
		Pattern p = Pattern.compile("\\w+");
		//创建Matcher对象
		Matcher m = p.matcher("abcd￥￥1234");
		//boolean result= m.matches();	//尝试将整个字符序列与该模式匹配
		//System.out.println(result);
		
		//boolean result= m.find();	//该方法扫描输入的序列，查找与该模式匹配的下一个子序列
		
		//System.out.println(m.find());
		//System.out.println(m.group());
		//System.out.println(m.find());
		//System.out.println(m.group());
	
		while(m.find()){
			System.out.println(m.group());	//group(),group(0)匹配整个表达式的子字符串
			System.out.println(m.group(0));
		}
		
	}
}

```



##### 分组

```java
package com.bjsxt.regex.test;

import java.util.regex.Matcher;
import java.util.regex.Pattern;

/**
 * 测试正则表达式对象中分组的处理
 */
public class Test2 {
	public static void main(String[] args) {
		//在这个字符串：abcd1234，是否符合指定的正则表达式：\w+
		//表达式对象
		Pattern p = Pattern.compile("([a-z]+)([0-9]+)");
		//创建Matcher对象
		Matcher m = p.matcher("abc123%%abcd234%abcde4567");
	
		while(m.find()){
			System.out.println(m.group());	//group(),group(0)匹配整个表达式的子字符串
			System.out.println(m.group(1));
			System.out.println(m.group(2));
		}
		
	}
}

```

find用法

https://www.bilibili.com/video/BV1Eq4y1E79W?p=4

##### 替换

```java
package com.bjsxt.regex.test;

import java.util.regex.Matcher;
import java.util.regex.Pattern;

/**
 * 测试正则表达式对象的替换操作
 */
public class Test3 {
	public static void main(String[] args) {
		//表达式对象
		Pattern p = Pattern.compile("[0-9]");
		//创建Matcher对象
		Matcher m = p.matcher("abc123%%abcd234%abcde4567");
		//替换
		String result= m.replaceAll("#");
		System.out.println(result);
	}
}

```



##### 分割

```java
package com.bjsxt.regex.test;

import java.util.regex.Matcher;
import java.util.regex.Pattern;

/**
 * 测试正则表达式对象的分割字符串的操作
 */
public class Test4 {
	public static void main(String[] args) {
		String str = "ab23jk123ji8890123asd";
		String[] arrs = str.split("\\d+");
		System.out.println(Arrays.toString(arrs));
	}
}

```



##### **手写网络爬虫（基本原理&乱码处理）**

```java
package com.bjsxt.regex.test;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.MalformedURLException;
import java.net.URL;
import java.nio.charset.Charset;
import java.util.ArrayList;
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

/**
 * 网络爬虫取链接	
 */
public class WebSpiderTest {
	
	/**
	 * 获得urlStr对应的网页的源码内容
	 * @param urlStr
	 * @return
	 */
	public static String  getURLContent(String urlStr,String charset){
		StringBuilder sb = new StringBuilder();
		try {
			URL url = new URL(urlStr);
			BufferedReader reader = new BufferedReader(new InputStreamReader(url.openStream(),Charset.forName(charset)));
			String temp = "";
			while((temp=reader.readLine())!=null){
				sb.append(temp);
			}
		} catch (MalformedURLException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
		return sb.toString();
	}
	
	
	public static List<String> getMatherSubstrs(String destStr,String regexStr){
		Pattern p = Pattern.compile(regexStr);	//取到的超链接的地址
		Matcher m = p.matcher(destStr);
		List<String> result = new ArrayList<String>();
		while(m.find()){
			result.add(m.group(1));
		}	
		return result;
	}
	
	
	public static void main(String[] args) {
		String destStr = getURLContent("http://www.163.com","gbk");
		
		//Pattern p = Pattern.compile("<a[\\s\\S]+?</a>");//取到的超链接的整个内容
		List<String> result = getMatherSubstrs(destStr, "href=\"([\\w\\s./:]+?)\"");
		
		for (String temp : result) {
			System.out.println(temp);
		}
		
	}
}

```



https://blog.csdn.net/qq_39636602/article/details/101236461

https://github.com/ziishaned/learn-regex/blob/master/translations/README-cn.md

https://regexr.com/





#### Ascii表

https://www.ascii-code.com/

https://www.regular-expressions.info/tutorial.html



#### 密码判断断言

必须包含一个字母或其他的字符

https://www.cnblogs.com/haoyul/p/12059737.html

https://www.bilibili.com/video/BV1nY4y1q7Qr?spm_id_from=333.337.search-card.all.click

https://www.bilibili.com/video/BV1oz4y1C7Uf?p=4

(?=.*[A-Za-z]+)[A-Za-z@\\/`'’‘,\\.\\(\\)\\-]{4,100}$



![image](https://github.com/noteforme/noteforme.github.io/assets/6995071/11cc4f59-d9af-4d83-8330-f9405b8ad936)

从这个图可以看到，需要中间至少需要一个字母


```
^(?=.*?[A-Z])(?=.*?[^A-Za-z0-9]).{6,12}$

(?=.*?[A-Z])
(?=xxx)是零宽断言，表示后面的字符串必须符合xxx这个正则表达式，但是不消耗字符串，实际匹配字符串的正则是.{6,12}即6到12位字符 
(?=.*?[A-Z])表示后面必须符号.*?[A-Z]这个 ，即必须有大写字母
整个正则表达式表示6到12位字符，必须有大写字母和不是字母数字的字符
```



https://zhidao.baidu.com/question/1609169242401476667.html



#### 正则优先级

下图 从上到下，从左到右的优先级

https://www.runoob.com/regexp/regexp-operator.html

https://zhidao.baidu.com/question/1609169242401476667.html



http://www.rexegg.com/regex-lookarounds.html





### kotlin regular



```kotlin
fun validation(pattern: String, str: String?): Boolean {
    return if (str.isNullOrEmpty()) {
        false
    } else Pattern.compile(pattern).matcher(str).matches()
}
```







### escape character



方括号（中括号）内的特殊字符不需要转义

即使加了转义字符，也不会起作用 `[\\.]` 还是表示点



```text
[\^\[\-\]\\]
```

会改变字符组含义的才需要转义

1、反斜线必须转义

2、方括号必须转义

3、「^」在首和「-」在中必须转义

所以以下常见的字符是不需要转义的

```as3
[aeiou]
[$.*+?{}()|]
[abc^123-]
```



https://www.zhihu.com/question/62542695

https://juejin.cn/s/%E6%AD%A3%E5%88%99%E4%B8%AD%E6%8B%AC%E5%8F%B7%E4%B8%AD%E7%89%B9%E6%AE%8A%E7%AC%A6%E5%8F%B7%E9%9C%80%E8%A6%81%E8%BD%AC%E4%B9%89%E5%90%97