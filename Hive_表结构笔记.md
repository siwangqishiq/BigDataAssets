Hive分区表Partition
	Partition对应与数据库的Partition列的密集索引
	对应子目录
	
	分区表  指定分区的条件
 	crate table student
	(
		id int,
		name string,
		gender char,
		math float,
		english float,
		physics float
	)
 
	创建分区表
	gender = 'M'   gender = 'F'
	
	创建一张基于性别的分区表
	create table partition_table
	(
		id int,
		name string,
	)	
	partitioned by (gender char)
	row format delimited fields terminated by ',';
	
	给分区表导入数据
	insert into table partitio_table 
	partition(gender = 'M')
	select id ,name , gender from student where gender = 'M';
	
	insert into partition_table 
	partition(gender = 'F')
	select id,name,gender where gender = 'F';
	
explain+SQL语句  查看执行计划 用于分析HSQL的执行效率

HIVE的外部表 External Table
	外部表=指向已经在HDFS中存在的数据 , 可以创建Partition
	与内部表在元数据的组织上是相同的 实际数据的存储规则则有较大差异
	外部表不会把数据移动到数据仓库中，只是与外部数据建立链接
	删除外部表时仅仅删除与数据建立的链接

	创建外部表
	create external table extern_table_name
	(
		id int,
		name string,
		age int
	)
	row format delimited fields terminated by ','
	location '/input';

HIVE桶表
	Bucket Table对数据进行hash 然后放到不同文件中存储
	提高查询速度 降低系统热块
	创建bucket table
	create table bucket_student_table
	(id int , name string , age int)
	clustered by(name) into 5 buckets;

HIVE视图
	viw 虚表 逻辑概念 建立在已有表的基础之上 简化复杂查询
	操作view  = 操作table
	
	create table dept
	(
		deptno int,
		name string
	)
	row format delimited fields terminated by ',';
	
	create table emp
	(
		no int,
		name string,
		job string,
		mgr string,
		hiredate date,
		sal int,
		comn int,
		deptno int
	)
	row format delimited fields terminated by ',';
	创建视图
	create view emp_info
	as 
		select  e.no , e.name , e.sal , e.sal *12 annlsal,d.name
		from emp e , dept d
		where e.deptno = d.deptno;
		
	desc emp_info;	
	HIVE不支持物化视图 所以View中不能插入数据
	  
