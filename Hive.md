Hive 笔记
	show tables --查看列表;

	show functions --查看函数列表;
		avg decode
	!clear 清理屏幕

desc 表名字  查看表结构
hive> !+linux操作命令

select * from table_name
eg : 	select * from test1; // 全表查询不会解析成MapReduce
	select name from test1;  --> MapReduce Task   run in hadoop

source /home/panyi/my.sql     执行sql文件

hive -s ＃hive的静默模式  不产生调试信息
hive -e 'select * from test1'  #hive执行一条命令

Hive 的数据类型
	基本数据类型
		tinyint/smallint/int 
		float / double
		字符串
		string 
		varchar
		char		

		create table person
		(
			pid int,
			pname string,
			married boolean,
			salary double,
		);

		desc person;

		create table test1
		(
			id long,
			cname varchar(20),
			cname2 char(20)
		);

	复杂数据类型
		Array 数组
		create table student 
		(
			sid int,
			sname string,
			grade Array<float>
		);
		desc student;
		
		Map集合
		create table student
		(
			id int,
			name string,
			grade Map<string,float>
		);
		desc student;

		create table student 
		(
			id int,
			name varchar(20),
			grades List<Map<string , float>>
		);
		desc student;
		
		Struct 结构类型
		create table student 
		(
			id int,
			name string,
			info Struct<name:string , age:int , sex:string>
		);
		{1 , "haha" , {'haha',11,'f'}}

	时间类型
		Date 日期  年月日
		Timestamp 时间戳

		select unix_timestamp()	#显示系统时间戳


HIVE的数据存储
	HIVE表对应hdfs上的文件
	
	表 视图
	内部表 Table
	
	create table t1	
	(
		id int,
		name string,
		age int
	);

	创建表指定保存位置
	create table t2 
	(
		id int,
		name string,
		age int
	) 
	location '/mytable/hive/t2';

	指定列与列的分隔符 
	create table t3
	(
		id int,
		name string
	)
	row format delimited fields terminated by ','
	
	子查寻创建表
	create table t4 
	as 
	select * from t2;
	  
	指定分隔符创建表	
	create table t5 
	as 
	select * from t2;
	row format delimited fields terminated by ','
	
	修改表结构
	alter table t1 add columns(englisg int);
	alter table t2 add columns(math int);
	
	删除表
	drop table t1
	
	
	
