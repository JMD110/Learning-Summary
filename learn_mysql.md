# MySQL
MySQL基础知识

### sql:结构化查询语言,是访问和处理数据库的标准计算机语言
  组织结构:数据库表  ->  一个或多个表 (每个表有一个名字标识)  ->  含有数据的记录行<br/>
  MySQL 因其开源及社区版免费的特点得到了广泛运用,MySQL 是最流行的关系型数据库管理系统之一，在 WEB 应用方面，
  MySQL是最好的 RDBMS (Relational Database Management System，关系数据库管理系统) 应用软件。<br/>
  在sql中大小写不敏感,所以我的代码中要是你发现上下文大小写对不上请包含(一个没有强迫症的程序员注)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;DML数据库操作语言: select/delete/update/insert<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;DDL数据库定义语言: alter/create/drop<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;聚合函数:max(列名)/min(列名)/count(列名)/sum(列名)/avg(列名)<br/>
### 一.安装
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Linux系统: ubuntu: sudo apt-get install mysql mysql-client<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;centos: yum install mysql-server<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;yum install mysql-devel<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;如果报错<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;yum list | grep mysql 看看是不是你的yum库中没有MySQL<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;如果没看见类似于mysql-server,mysql-devel的,就先执行:<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rpm -ivh mysql-community-release-el7-5.noarch.rpm<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;windows: https://www.mysql.com/ 到官网下载后(学习请选社区版),可选择一路默认安装,如果你不懂最好什么都别选<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mac: 官网下载后也是一路默认安装  <br/>

### 二.运行及配置
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;启动服务: 命令行提示符(以管理员身份运行)下,运行net start mysql57  <br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;配置环境变量: 计算机->属性->高级系统设置->环境变量->系统环境变量->path->编辑 <br/>
(粘贴mysql的安装目录,默认目录为C:\Program Files\MySQL\MySQL Server 5.7\bin)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;进入mysql: mysql -u root -p 输入你的密码 password: <br/>


### 三.Database数据库
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; show databases; 可以查看你的所有数据库 <br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; create Database 数据库名称  ; -->新建数据库 <br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 举例: create database STU default CHARSET utf8; 建一个名为STU的数据库,默认UTF-8格式 <br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; use 数据库名称 ;              -->使用数据库 <br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 举例: use STU   <br/>


### 四.Table
create table 表名称 (列1名称 列类型,列2名称 列类型....);注意每列用符号','隔开,每句用';'结尾 <br/> <br/>
例如建一个有编号/学生姓名/年龄/性别(用1表示男,0表示女)的学生表 建一个有编号/家长姓名/家长电话/学生编号的家长表:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;举例: create table student (stuid tinyint not null auto_increment, stuname varchar(4) not null,stuage tinyint not null,stusex bit default 1,primary key(stuid)); <br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;举例: create table stuFamily (famid tinyint auto_increment, parentname varchar(4) not null, parenttel char(11), sid tinyint, primary key(famid),foreign key(sid) references student(stuid)); <br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;注意千万别用中文符号例如逗号括号这些,新手可以在自己使用的输入法中将中文使用英文符号选上. <br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;主键的意义为唯一标识,类似于每个学生的学号不同,每个人的身份证号码不同,对应到数据库表中能找到唯一的行. <br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;外键的意义为关联数据表,类似于如果有一个学生表,有一个学生家长表,如果要将家长表联系到学生的话,就需要在家长表中创建一个外键, <br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;外键可以设置为学生的学号,意思就是这个家长能够对应到学生表中唯一的学生. <br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;注意外键的表应该先创建,因为你没有该表,怎么联系到该表呢? <br/>
select * from student; <br/>
select * from stuFamily; <br/>
查看你建的表 <br/>

### 五.语句
&nbsp;&nbsp;基础(增insert删delete改update查select) <br/>
&nbsp;&nbsp;增行: insert into 表名称 (列1名称,列2名称...) values (列1值,列2值...); <br/>
&nbsp;&nbsp;更改行: UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值; <br/>
&nbsp;&nbsp;更改类型: alter table 表名称 modify column 列名称 类型;   <br/>
&nbsp;&nbsp;删行: DELETE FROM 表名称 WHERE 列名称 = 值;  -->删除列=值的那一行 <br/>
	      DELETE * FROM 表名称; -->删除表中所有行
&nbsp;&nbsp;查询: <br/>
select * from 表名称  -->查看全表 <br/>
select 列名称1 列名称2 from 表名称 -->取出该表某列 <br/>
select * from 表名称 where 列名称=值 -->	取出该列值为某值的全部行,如果是主键列的话是不是一定会取出唯一的行?知道主键的作用了吗? <br/>
select max(列名) from 表名称  -->取出该表某列最大值 <br/>
select min(列名) from 表名称  -->取出该表某列最小值 <br/>
select avg(列名) from 表名称  -->取出该表某列平均值 <br/>
select sum(列名) from 表名称  -->取出该表某列总值 <br/>
select * from 表名称 having 列名称>avg(列名称)  -->取出该表某列大于该列平均值的行的全部数据 <br/>
举例:select count(列名) from 表名称 group by(列名) -->通过列名2进行分组,比如一个年级学生表, <br/>
年级里有六个班,我们按班来分组,查询每个班有多少学生 <br/>
类似于: select count(stuclass) from tbGradeStu group by(stuclass) <br/>
select * from 表名称 order by (列名)      -->以某列进行排序 默认是从小到大,从a-z,在后面加上DESC 可以反序 <br/>
