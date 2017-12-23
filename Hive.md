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


	





