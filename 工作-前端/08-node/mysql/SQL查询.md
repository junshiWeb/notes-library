常用

- as：别名

## 条件语法

#### 条件

- 使用where子句对表中的数据筛选，结果为true的行会出现在结果集中
- 语法如下：

```
select * from 表名 where 条件;
```

#### 比较运算符

- 等于=
- 大于>
- 大于等于>=
- 小于<
- 小于等于<=
- 不等于!=或<>

#### 逻辑运算符

- and：并 
- or：或
- not：不包含

#### 模糊查询

- like：模糊
- %表示任意多个任意字符
- _表示一个任意字符

#### 范围查询

- in 表示在一个非连续的范围内，表示包含什么内容

- between ... and ... 表示在一个连续的范围内，表示在什么什么之间的

#### 空判断

- 注意：null 与' '是不同的
- 判空 is null

- 判非空is not null

#### 优先级

- 小括号，not，比较运算符，逻辑运算符
- and 比 or 先运算，如果同时出现并希望先算 or，需要结合 () 使用

## 排序

- 语法：

```sql
select * from 表名 order by 列1 asc|desc,列2 asc|desc,...
```

- 将行数据按照列1进行排序，如果某些行列1的值相同时，则按照列2排序，以此类推，默认按照列值从小到大排列
- asc从小到大排列，即升序
- desc从大到小排序，即降序

## 聚合

- 为了快速得到统计数据，提供了5个聚合函数
- count(*) 表示计算总行数，括号中写星与列名，结果是相同的

```sql
select count(*) from students;
```

- max(列)表示求此列的最大值

```sql
select max(column) from table where condition;
```

- min(列)表示求此列的最小值

```sql
select min(column) from table where condition;
```

- sum(列)表示求此列的和

```sql
select sum(column) from table where condition;	
```

- avg(列)表示求此列的平均值

```sql
select avg(column) from table where condition;
```

## 分组

- 按照字段分组，表示此字段相同的数据会被放到一个组中
- 分组后，只能查询出相同的数据列，对于有差异的数据列无法出现在结果集中
- 可以对分组后的数据进行统计，做聚合运算
- 语法：

```
select 列1,列2,聚合... from 表名 group by 列1,列2,列3...
```

- eg

```sql
select gender as 性别,count(*)
from students
group by gender;
```

**分组后的数据筛选**

- 语法：

```sql
select 列1,列2,聚合... from 表名
group by 列1,列2,列3...
having 列1,...聚合...
```

- having后面的条件运算符与where的相同
- eg

```
select gender as 性别,count(*)
from students
group by gender
having gender=1;
```

**对比where与having**

- where 是对 from 后面指定的表进行数据筛选，属于对原始数据的筛选
- having 是对 group by 的结果进行筛选

## 分行

- limit 当数据量过大时，在一页中查看数据是一件非常麻烦的事情
- 语法：

```
select * from 表名
limit start,count
```

- 从start开始，获取count条数据

**示例：分页**

- 已知：每页显示m条数据，当前显示第n页
- 求总页数：此段逻辑后面会在python中实现
  - 查询总条数p1
  - 使用p1除以m得到p2
  - 如果整除则p2为总数页
  - 如果不整除则p2+1为总页数
- 求第n页的数据

```
select * from students
where isdelete=0
limit (n-1)*m,m
```

## 连接查询

连接查询分类如下：
- 表A inner join 表B：表A与表B匹配的行会出现在结果中
- 表A left join 表B：表A与表B匹配的行会出现在结果中，外加表A中独有的数据，未对应的数据使用null填充
- 表A right join 表B：表A与表B匹配的行会出现在结果中，外加表B中独有的数据，未对应的数据使用null填充

- 在查询或条件中推荐使用“表名.列名”的语法
- 如果多个表中列名不重复可以省略“表名.”部分
- 如果表的名称太长，可以在表名后面使用' as 简写名'或' 简写名'，为表起个临时的简写名称

语法

```sql
select table_1.col,table_2.col from table_1 
inner join table_2 on condition 
```

#### 练习

- 查询学生的姓名、平均分

```sql
select students.sname,avg(scores.score)
from scores
inner join students on scores.stuid=students.id
group by students.sname;
```

- 查询男生的姓名、总分

```
select students.sname,avg(scores.score)
from scores
inner join students on scores.stuid=students.id
where students.gender=1
group by students.sname;
```

- 查询科目的名称、平均分

```
select subjects.stitle,avg(scores.score)
from scores
inner join subjects on scores.subid=subjects.id
group by subjects.stitle;
```

- 查询未删除科目的名称、最高分、平均分

```
select subjects.stitle,avg(scores.score),max(scores.score)
from scores
inner join subjects on scores.subid=subjects.id
where subjects.isdelete=0
group by subjects.stitle;
```

## 子查询

**什么是子查询?**

 当一个查询是另一个查询的条件时,这个查询称之为子查询(内层查询)

**什么时候用？**

 当查询需求比较复杂，一次性查询无法得到结果，需要多次查询时

语法

```sql
select col from table_1 where  table_2_id in 
(select id from table_2 where condition);
```

**注意**

 in中的子查询只能包含一个列

 例如：查询财务部有哪些人

**关键字：exists**

exists 后跟子查询，子查询有结果是为True，没有结果时为False。为True时外层执行，为False外层不执行

**如何使用？**

```sql
select * from table_1 where exists (select * from table_2 where condition);
```

前面 exists 后面 如果 *后面* 查询有结果时，*前面* 才会执行

## 视图

最好不使用，会影响数据

对于复杂的查询，在多次使用后，维护是一件非常麻烦的事情

视图本质就是对查询的一个封装

- 定义视图

```sql
create view stuscore as 
select students.*,scores.score from scores
inner join students on scores.stuid=students.id;
```

- 视图的用途就是查询

```
select * from stuscore;
```

### 操作

```
-- 查询视图内容等同于查询表操作
SELECT * from bookallinfo where cataory = '历史传记';
-- 视图实现模糊查找
SELECT * from bookallinfo where bookname like "%小%";

-- 更新多字段
UPDATE booktable SET bookname = "小时代1",authorid=0,score = NULL  where id = 2;

-- 删除
-- 逻辑删除和物理删除

-- 逻辑删除小时代书
UPDATE booktable set isdelete = "true" where id = 2

-- 物理删除
-- DELETE from booktable WHERE bookname = "鬼吹灯"
DELETE from booktable
```

 