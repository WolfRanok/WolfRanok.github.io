---
layout: post
title: MySql 学习笔记
color: brown
permalink: mysql
thumbnail: assets\img\thumbnails\feature-img\mysql.png
---
MySQL是一种关系型数据库管理系统，关系数据库将数据保存在不同的表中，而不是将所有数据放在一个大仓库内，这样就增加了速度并提高了灵活性。

---
## 前言
本人比较懒，所以专门挑了一个篇幅比较少的MySql来写博客，主要还是针对笔记的性质来写的。如果有错欢迎指正。
---

## MySql 基本语法
#### 1.分组
`GROUP BY` 字段名 [`HAVING` 条件表达式]

#### 2.去重
在 `select`的字段前面加上`distinct`就可以去重

#### 3.插入多行数据

格式：<br>
`insert into` 表名[（字段名1，字段名2,…）] `values`(值$$a_1$$，值$$b_1$$,…), (值$$a_2$$,值$$b_2$$,…)

示例：
```sql
insert into mywork
values("小明",18),("小红",20)
```

#### 4.外连接
语法：<br>
`select` 字段列表 `from` 表1 [inner] `join` 表2 `on` 连接条件;
示例:

```sql
select * 
from wuhan.commercialhousing 
join secondhouse on district regexp qy
limit 10;
```

同理还有左外连接：`left join`，右外连接：`right join`

#### 5.排序

排序语句：`order by` 字段值`[ desc | asc]`
其中 `asc`是表示升序（默认），表示降序

示例：
```sql
select customer_number
from Orders
group by customer_number
order by COUNT(*) desc
```

#### 6.if语句

语法：`IF(expr1,expr2,expr3)`

如果 expr1 是`TRUE` (或者expr1 <> 0 且 expr1 <> NULL)，则 IF()的返回值为expr2;<br> 否则返回值则为 expr3。IF() 的返回值为数字值或字符串值，具体情况视其所在语境而定。

#### 7.ifnull语句

语法：`IFNULL(expr1,expr2)`
expr1不为`NULL`，则 IFNULL() 的返回值为expr1; 否则其返回值为 expr2。<br>IFNULL()的返回值是数字或是字符串，具体情况取决于其所使用的语境。

#### 8.正则语句

关键字：`regexp`

使用语法：被检测字符串 `regexp [binary]` 正则语句
不区分大小写（即大写和小写都匹配）。为区分大小写，可以使用 BINARY 关键字<br>例如：
```sql
WHHERE name REGEXP BINARY 'Hern .000'
```

#### 9.存在判断语句 exists

当我们只需要判断某些满足特定条件的数据是否存在时，为了提高效率，我们不需要将所有的数据捞出来判断，只需要判断是否存在就可以了。
采用exists即可满足需求。<br>
示例：<br>
```sql
select exists (SELECT *
        from  a 
        where
        money>0 and time>'2021-03-05';
)
```

## mysql常用函数

#### 日期比较函数：datediff

语法：`DATEDIFF(date1,date2)`
参数说明<br>
date1: 比较日期1<br>
date2: 比较日期2<br>

DATEDIFF函数返回date1 - date2的计算结果，date1和date2两个参数需是有效的日期或日期时间值;如果参数传递的是日期时间值，DATEDIFF函数仅将日期部分用于计算，并忽略时间部分(只有值的日期部分参与计算)

示例：
```sql
SELECT DATEDIFF('2022-04-29','2022-04-30'); --返回 -1
SELECT DATEDIFF('2022-04-30','2022-04-29'); --返回 1
```

#### 日期加减函数：date_add 

语法：`date_add(‘某个日期时间’,interval 1 时间种类名)`<br>
示例：

```sql
select date_add(data, interval 1 year); --加1年
select date_add(fata, interval 1 month); --加1月
```

quarter:季，week:周，day:天，hour:小时，minute:分钟，second:秒，microsecond:毫秒<br>
注：也可以不用变量，直接加减某个时间，如：select date_add(‘1998-01-01’, interval 1 day);

#### 字符串拼接：concat

将给入的参数逐一拼接<br>
例如：
```sql
concat(‘%’,’abc’,’%’) --结果为%abc%
```
#### 字符串与日期的相互转换
使用语法：<br>
`DATE_FORMAT(date,format) `日期转字符串<br>
`STR_TO_DATE(str,format) `字符串转日期<br>
示例：

```sql
select DATE_FORMAT(now(),'%Y-%m-%d %H:%i:%s');
```
返回：2022-12-01 10:07:41

```sql
select str_to_date('2022-8-7','%Y')
```
返回：2022-00-00<br>
因为这里只获取到了年份，但是作为datetime对象需要补全月份和日所以会有-00-00出现。

#### 组内字符串拼接 group_concat

语法：<br>
```sql
GROUP_CONCAT([DISTINCT] column1 [ORDER BY column2 ASC|DESC] [SEPARATOR seq])
```

将分组中column1这一列对应的多行的值按照column2 升序或者降序进行连接，其中分隔符为seq<br>
如果用到了DISTINCT，将表示将不重复的column1按照column2升序或者降序连接<br>
如果没有指定SEPARATOR的话，也就是说没有写，那么就会默认以 ','分隔

## 技巧语法

#### 查询排名前n的数据

使用`limit` n语句实现（该语句需要放在查询结果的最后）

示例：

```sql
SELECT * FROM wuhan.secondhouse limit 10;
```

#### 使用正则配对字符串

使用`regexp`关键字实现
格式： `字段值 regexp 正则字符串`
示例：

```sql
select distinct district,house_type,wq_area,wq_num,yqy_area,yqy_num
from commercialhousing
where district regexp '江岸';
```