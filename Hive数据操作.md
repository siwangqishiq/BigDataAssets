Hive的数据导入
	load命令
	load data [local] inpath 'filepath' [override]
	into table tablename [partition (partcol = val,...)]
	
	eg 导入数据
	load data local inpath '/root/data/student01.txt'
	into table t2;

	load data local inpath '/root/data/student01.txt'
	into table t3;

	将/root/data下所有数据文件导入t3 且覆盖原有数据
	load data local inpath '/root/data'
	override into table t3;
	
	导入hdfs中的数据文件
	load data inpath '/input/student01.txt'
	override into table t3;
	
	导入数据到分区
	load data local inpath '/input/data/data1.txt'
	into table partition_t1 partition(gender = 'M')
	
	load data local inpath '/input/data/data2.txt'
	into table partition_t1 partition(gender = 'F')

	sqoop组建导入数据
		sqoop数据导入和导出的开源框架
		

Hive 数据查询
	简单查询
		select 语法
		select * from emp;
		select empno,ename,sal from emp;
		
		支持算数表达式的Sql
		select empno,ename,sal , 12 * sal from emp;
		
		nvl函数  nvl(a , b)若a为null 设a = b;	
		select empno,ename,sal ,com , 12 * sal , 12 * sal + nvl(com , 0) from emp;
		判断是否为null
		select empno,ename,sal , 12 * sal from emp where com is null;
		
		distinct去掉重复记录
		select distinct deptno from emp;
		
	Fetch Task无函数 无排序 针对简单查询提高效率
	set hive.fetch.task.conversion = more;
									
	过滤排序
	Hive内置函数

Java客户端自定义函数
		
