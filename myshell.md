# Shell脚本编程基础
* * *
### shell概念:
 shell是一个用C语言编写的程序,他是用户使用Linux的桥梁,它是一种命令语言,同事也是一种编程语言.用户可以通过Shell访问操作系统和内核服务.Linux的Shell种类众多,Bash是大多数Linux系统默认的Shell,所以我以Bash为例学习shell脚本编程.
* * *
### shell变量:

**变量的命名**
1.  命名只能使用,字母/数字/下划线
2.  中间不能有空格
3.  不能使用标点符号
4.  不能与关键字重合

**变量操作**
>1. 使用: $变量名 或者 ${变量名}

	#!/bin/bash            # 表示为bash的shell  也可以写成#!/bin/sh
	a=4
	b=5
	c=\`expr $a + $b\`
	echo $c

2. 设置只读变量: 变量名 readonly
3. 删除变量: unset 变量名
4. 变量的赋值用'=',需要注意的是等号两边不要有空格,比如a=1是对的,但是a = 1或a= 1都是错的,'command not found'

**变量的分类**
1. 局部变量 局部变量在脚本或命令中定义，仅在当前shell实例中有效，其他shell启动的程序不能访问局部变量。
2. 环境变量 所有的程序，包括shell启动的程序，都能访问环境变量，有些程序需要环境变量来保证其正常运行。必要的时候shell脚本也可以定义环境变量。
3. shell变量 shell变量是由shell程序设置的特殊变量。shell变量中有一部分是环境变量，有一部分是局部变量，这些变量保证了shell的正常运行

**特殊变量**
有些变量是一开始执行脚本时就会设定,且不能被修改,但我们不叫它只读的系统变量,而叫它特殊变量
$\* 这个程序的所有参数<br/>
$# 这个程序的参数个数<br/>
$$ 这个程序的PID<br/>
$! 执行上一个后台程序的PID<br/> 
$? 执行上一个指令的返回值<br/>
* * *
### shell中常用数据类型
1. 字符串: 
*  可以使用单引号也可以使用双引号,单引号表示原样字符串,单引号中变量或者转义符都会无效,单引号里也不能出现单引号;
*  提取字符串长度 ${#变量名}
*  字符串切片 ${变量名:开始位置:结束位置}

str1='abc'<br/>  
str2="$str1"<br/>
str3='$str1'<br/>
echo $str1 $str2 $str3 #输出abc abc $str1<br/>
echo ${#str1} #输出3<br/>
echo ${str1:1:2} #输出bc 开始位置1 结束位置2 编程语言中一般都是以0是开始的<br/>

2. 数组:
*  数组的定义: 变量名=(值1 值2... 值n)
*  数组的读取: ${变量名[下标]} 或 取所有元素用${变量名[@]}
*  数组的长度: ${#变量名}

array1=(1 3 5 7 9) #注意数组中每个值用空格隔开而不是逗号<br/>
echo $array1  #输出1 默认下标0<br/>
echo ${array[4]}  #输出9<br/>
echo ${array1[@]}  #输出1 3 5 7 9<br/>
echo ${#array1[@]} #输出5<br/>
echo ${#array1}  # 输出1 取的是单个元素 默认的下标是0 单个元素长度为1<br/>

3. 注释:
*  以#开头的就是注释,会被解释器直接忽略

* * *
### shell传参

<table>
<tr><td>参数处理</td><td>说明</td> 	</tr>
<tr><td>$# </td><td>	传递到脚本的参数个数</td></tr>
<tr><td>$*</td><td>以一个单字符串显示所有向脚本传递的参数。如"$\*"用「"」括起来的情况、以"$1 $2 … $n"的形式输出所有参数。</td></tr>
<tr><td>$$ </td><td>脚本运行的当前进程ID号</td></tr>
<tr><td>$! </td><td>后台运行的最后一个进程的ID号</td></tr>
<tr><td>$@ </td>	<td>与$\*相同，但是使用时加引号，并在引号中返回每个参数。如"$@"用「"」括起来的情况、以"$1" "$2" … "$n" 的形式输出所有参数。</td></tr>
<tr><td>$-</td><td>显示Shell使用的当前选项，与set命令功能相同。</td></tr>
<tr><td>$?</td><td>显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。</td></tr>
</table>

* * *
### shell运算符

* 由于原生bash不支持简单的数学运算,但是可以通过其他命令实现,例如awk/expr,其中expr最常用,expr是一款表达式计算工具,使用时要用撇号\`包起来(撇号就是键盘上1左边的那个),而且需要注意的是它有严格的语法规范,表达式与运算符之间一定要有空格!例如\`expr $a + $b\`是对的,但是\`expr $a+$b\`是错误的!

1. 算数运算符:

<table>
<tr>
	<td>运算符</td>
	<td>说明</td>
	<td>举例</td>
</tr>
<tr>
	<td>+</td>
	<td>加法</td>
	<td>`expr $a + $b`</td>
</tr>
<tr>
	<td>-</td>
	<td>减法</td>
	<td>`expr $a - $b`</td>
</tr>
<tr>
	<td>*</td>
	<td>乘法</td>
	<td>`expr $a \* $b`</td>
</tr>
<tr>
	<td>/</td>
	<td>整除法</td>
	<td>`expr $a / $b` 如`expr 8 / 3`结果为2</td>
</tr>
<tr>
	<td>%</td>
	<td>取余</td>
	<td>`expr $a % $b`</td>
</tr>
<tr>
	<td>=</td>
	<td>赋值</td>
	<td>a=$b</td>
</tr>
<tr>
	<td>==</td>
	<td>相等</td>
	<td>$a == $b 判断是否相等 相等返回true 不相等返回false</td>
</tr>
<tr>
	<td>!=</td>
	<td>不相等</td>
	<td>$a != $b 相等返回false 不相等返回true</td>
</tr>
</table>

* * *
2. 关系运算符
关系运算符只支持数字,不支持字符串,除非字符串的值是数字.

<table>
<tr>
	<td>运算符</td>
	<td>说明</td>
</tr>
<tr>
	<td>-eq</td>
	<td>检测两个数是否相等,相等返回true</td>
</tr>
<tr><td>-ne</td>
	<td>检测两个数是否不等于,不等返回true</td>
</tr>
<tr>
	<td>-gt</td>
	<td>检测左边的数是否大于右边的,是就返回true</td>
</tr>
<tr>
	<td>-lt</td>
	<td>检测左边的数是否小于右边的,是就返回true</td>
</tr>
<tr>
	<td>-ge</td>
	<td>检测左边的数是否大于等于右边的,是就返回true</td>
</tr>
<tr>
	<td>-le</td>
	<td>检测左边的数是否小于等于右边的,是就返回true</td>
</tr>
</table>

3. 布尔运算:

! : 非运算符,[!true] 返回false<br/>
-o: 或运算符,任一true 返回true <br/>
-a: 与运算符,任一为false 返回false<br/>


4. 逻辑运算符:

&& 逻辑的AND<br/>
|| 逻辑的OR<br/>

5. 字符串运算符

= 	检测两个字符串是否相等，相等返回 true <br/> 
!= 	检测两个字符串是否相等，不相等返回 true <br/> 	
-z 	检测字符串长度是否为0，为0返回 true <br/>
-n 	检测字符串长度是否为0，不为0返回 true <br/>
str 检测字符串是否为空，不为空返回 true 举例 a='abc' [$a]返回ture<br/>

* * *
### shell命令
1. shell echo命令: 用于字符串的输出
*  echo abc 和 echo "abc" 是一样的

*  可以显示普通字符串\转义字符\变量

echo "Hello world"  #返回Hello world<br/>
text="Hello world"<br/>  
echo $text          #返回Hello world<br/>
echo \"Hello world\"#返回"Hello world"<br/>

*  可以定向至文件
	echo "Hello world" > test.log   会将"Hello world"定向输出到test.log中

*  可以显示命令执行结果
	echo `data`    #注意是撇号,结果将显示目前的日期
	echo `expr 2 + 3`   #执行结果5

2. shell printf命令:

*  可以格式化字符串输出 格式替代符(%s %c %d %f)
*  可以转义序列
	<table>
		<tr>\a 警告字符</tr>
		<tr>\b 后退</tr>
		<tr>\c 抑制,结尾不换行且后面的格式字符串中的字符都会被忽略</tr>
		<tr>\f 换页</tr>
		<tr>\n 换行</tr>
		<tr>\r 回车</tr>
		<tr>\t 水平制表符</tr>
		<tr>\v 垂直制表符</tr>
		<tr>\\\ 一个 \</tr>
	</table>

3. shell test命令:
test 命令用于检查某个条件是否成立，它可以进行数值、字符和文件三个方面的测试。格式为 test 条件语句
* 测试字符串

 test str1==str2   测试两个字符串是否相同<br/>
 test str1 !=str2  测试两个字符串是否不同<br/>
 test str1         测试是否为字符创<br/>
 test -n str1或test -z str1  测试是否为空的字符串<br/>

* 测试整数

test int1 -eq int2 测试是否相等<br/>
test int1 -ne int2 测试是否不等<br/>
test int1 -le int2 测试是否小于等于<br/>
test int1 -lt int2 测试是否小于<br/>
test int1 -ge int2 测试是否大于等于<br/>
test int1 -gt int2 测试是否大于<br/>

* 测试文件

test -d file 测试是否为目录<br/>
test -f file 测试是否为文件<br/>
test -x file 测试是否是可执行文件<br/>
test -r file 测试是否是可读文件<br/>
test -w file 测试是否是可写文件<br/>
test -e file 测试文件是否存在<br/>
test -s file 测试文件是否为空 <br/>
可简写 如 test -x file 可简写为 [ -x file ] 注意中括号旁一定加空格把执行命令括起来 <br/>
* * *

### shell 循环与分支

>1. 分支: if 和 if else 和 if elif else

	if 条件语句
	then
		条件为真执行语句
	fi
	也可以这样写为一行:if 条件语句; then 条件为真执行语句;fi   
	下面同理要么换行要么用';'

	if 条件语句
	then 
		条件为真执行语句
	else
		条件为假执行语句
	fi

	if 条件1语句
	then
		条件1为真执行语句
	elif 条件2语句
	then
		条件2为真执行语句
	else
		条件1与条件2都为假执行语句
	fi


>2. 循环语句: for循环 while循环 until循环 case循环
跳出循环break 跳出本次循环 continue

	举例说明:返回0到100的整数和
	#! /bin/bash
	sum=0
	for ((i=0; i<=100; i++))
	do
		sum=`expr $sum + $i`
	done
	echo $sum  #返回5050

	#! /bin/bash
	i=0
	while(($i<=3))
	do
		echo $i
		let "i++"
	done
	运行脚本,输出:
	0
	1
	2
	3


	
