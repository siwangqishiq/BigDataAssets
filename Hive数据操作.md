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
		where语句 
		select * from emp where empno = 10;
		select * from emp where name = 'King';
		select * from emp where deptno = 10 and sal < 100;
		explain 'select * from emp where empno = 10';
		
		模糊查询
		select * from emp where name like 'S%';
		
		排序
		order by
		select empno,name,sal from emp order by sal;
		select empno,name,sal from emp order by sal desc;				
		order by + 列名 or 表达式 or 别名 or 序号
		select empno,name,sal ,sal * 12 annsal from emp order by annsal;
		select empno,name,sal ,sal * 12 annsal from emp order by 4;		
		上面语句 需要开启 set hive.groupby.orderby.position.alias = true	
			
	Hive内置函数
		数学函数 round 四舍五入
					select round(34.11 ,2) 
				ceil 向上取整
				floor 向下取整
		字符函数
			lower 转小写
			upper 转大写
			length 字符串长度
			concat 字符串拼接
			substr 求子
			trim 去空格
			lpad 左填充
			rpad 右填充
		
		收集函数
			size(map(<key,value>,<key,value> ,...)) map集合的长度
		转换函数
			cast
			cast(1 as bigint)
			cast(1 as float)
			cast('2015-04-10' as date)
		日期函数
			to_date 取出字符串中的日期
			year
			month
			day
			weekofyear
			datediff
			date_add
			date_sub
		条件函数
			coalesce 从左往右找到第一个不是null的
			case...when...then...end
			select name,job,sal,
				case job when 'PRESIDENT' then sal + 1000
						 when 'MANAGER' then sal +800	
						 else sal + 400 
			from emp;
		聚合函数
			count
			sum
			min
			max
			avg
		表生成函数
			explode 转化键值对为单独行
			select explode(map(1 , 'value' , 2 , 'Value2'))
			result:
				1 value
				2 Value2

Hive表连接
	等值连接
		
	不等值连接
		between ... and ...
	外连接
		group by ...
		select d.deptno,d.dname,cout(e.empno)
		from emp e right outer join dept d
		on(e.deptno = d.deptno)
		group by d.deptno,d.name;
	自连接

Hive子查询
	from where 子查询
	
Hive自定义函数
		
