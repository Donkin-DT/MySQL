###### MySQL 基础😀

```mysql
1.数据库相关概念      
	DBMS
	DB
	SQL
2.数据库存储数据特点
3.初识MySQL
	MySQL产品介绍        
	MySQL产品安装 😀              
	MySQL服务启动和停止😀    
	MySQL服务的登录和退出😀        
	MySQL的常见命令和语法规范
4.DQL语言学习              
	基础查询 😀                  
	条件查询 😀 	  			
	排序查询 😀 	  				
	常见函数 😀                     
	分组函数 😀                     
	分组查询 😀		   			
	连接查询 😀	 				
	子查询 😀                      
	分页查询 😀                   
	union联合查询😀					
5.DML语言学习😀                 
	插入语句😀						
	修改语句😀						
	删除语句😀						
6.DDL语言学习  
	库和表的管理😀	 				
	常见数据类型介绍          
	常见约束  	  			
7.TCL语言学习
	事务和事务处理
```

###### MySQL

```mysql
好处:
	1.持久化数据到本地
	2.可以实现结构化查询，方便管理

相关概念:😀
	1.DB：数据库，保存一组有组织数据的容器
	2.DBMS：数据库管理系统，又称为数据库软件（产品），用于管理 DB 中的数据
	3.SQL:结构化查询语言，用于 DBMS 通信语言

存储特点:
	1.将数据放到表中，表再放到库中
	2.一个数据库中可以有多个表，每个表都有一个的名字，用来标识自己。表名具有唯一性
	3.表具有一些特性，这些特性定义了数据在表中如何存储，类似java中 “类”的设计
	4.表由列组成，我们也称为字段。所有表都是由一个或多个列组成的，每一列类似java 中的”属性”
	5.表中数据是按行存储的，每一行类似于java中的“对象”

MySQL产品介绍和安装：😀

MySQL服务启动和停止：😀
	方式1：
		计算机——右击管理——服务
	方式2：
		管理员身份运行命令行😀
			net start 服务名
			net stop 服务名
			
MySQL服务登录和退出：   
	方式1：
		通过 mysql 自带客户端，只限于root用户

	方式二：
		通过 windows 自带客户端
		登录：
			mysql 【-h主机名 -P端口号 】-u用户名 -p密码

	退出：
		exit 或 ctrl + C
		
MySQL语法规范：😀
	1.不区分大小写,建议关键字大写，表名和列名小写😀
	2.每条sql语句结尾，建议使用分号
	3.sql注释
		单行注释：
			#注释文字
		单行注释:
			-- 注释文字
		多行注释：
			/*注释文字*/
	4.每条 sql 语句可以换行写，但关键字、表名、列名不能拆开

SQL语言分类：😀
	1.DQL语言：Data Query Language 数据查询语言😀
		select
		
	2.DML语言：Data Multipulation Language 数据操作语言😀
		insert、update、delete
		
	3.DDL语言：Data Define Language 数据定义语言😀
		create、drop、alter
			
	4.DCL语言：Data Control Language 数据控制语言
		TCL语言：Transaction Control Language事务控制语言
			commit、rollback
```

###### DQL语言😀

```mysql
常见命令 😀
	1.查看当前所有数据库
		SHOW DATABASES;
		
	2.打开指定库
		USE 库名;
		
	3.查看当前库所有表
		SHOW TABLES;
		
	4.查看其它库所有表
		SHOW TABLES FROM 库名;
		
	5.创建表
		create table 表名(
			列名 列类型,
			列名 列类型，
             ...
		);

		CREATE TABLE stuinfo(
			id INT,
			NAME VARCHAR(20)
		);
		
	6.查看表结构 😀
		DESC 表名;
		
	7.查看服务器版本
		方式1：登录 mysql 服务端
			SELECT VERSION();
			
		方式2：没有登录到 mysql 服务端
			mysql --version
			或
			mysql -V

基础查询😀
	USE myemployees;
	
	语法：
		select 查询列表 【from 表名】;

	类似：
		System.out.println(打印内容);

	特点：
		1.查询列表可以是单个字段、多个字段、所有字段、常量、函数、表达式，或者上述组合
		2.查询结果为虚拟表，并不真实存在


	案例：
		1.查询单个字段（列）
			SELECT last_name FROM employees;

		2.查询多个字段
			SELECT email,salary,last_name FROM employees;

		3.查询所有字段
			SELECT * FROM employees;

		4.查询常量值
			SELECT 'john';
			SELECT '中国',last_name FROM employees;
			
		5.查询表达式
			SELECT 100+2;
			SELECT 100*6;
			
		6.查询函数（方法）
			SELECT VERSION();
			SELECT DATABASE();

		7.起别名😀
			方式1：使用 as 关键字
				SELECT email AS 邮箱,last_name AS 员工姓名,first_name FROM employees;
			
			方式2：使用空格
				SELECT email 邮箱,last_name  员工姓名,first_name FROM employees;
				
		8.关于 + 的使用😀
			+ 仅仅只有一个作用：加法运算
				select 100+23;
			如果两个操作数都是数值型，结果就是加法运算的结果
				select 100+'12';
			如果两个操作数中有字符型，则需要先将字符型转换成数值型，如果转换成功，则做加法运算，否则该字符值转换成 0，然后再做加法运算
				select 'abc'+12;
			如果两个操作数中有一个为 null，则结果肯定是 null。
				select null+'2er';

			# +  [错误] SELECT first_name+last_name  AS  姓名 FROM employees;
			使用函数 concat 拼接😀
				SELECT CONCAT(first_name,last_name) AS 姓名 FROM employees;
		
		9.去重😀
			SELECT DISTINCT department_id FROM employees;
			
条件查询😀
	备注：😀
		字符型和日期型常量值要求使用单引号引起来

	语法：
		select 查询列表 from 表名 where 条件;
		
	分类：😀
		1.按条件表达式进行查询
			> < >= <= =  <> 

		2.按逻辑表达式进行查询
			and  or  not
			
		3.模糊查询😀
			like:一般搭配通配符使用，用于判断数值型或字符型数据（字符型较多）
				%:任意多个字符，包含0个或多个
				_:任意单个字符
				
		 	in：用于判断某个字段的值是否属于列表中的其中一项
				语法：
					where 字段 in(值1，值2,值3)
				
			between and:判断某字段的值是否在...之间,一般用于数值型判断
				语法：
					where 字段 between 值1 and 值2（包含:值1,值2）
					
			is null/is not null
			
	案例:
		1.按条件表达式查询
			#需求1：查询工资>10000的员工信息
				SELECT * FROM employees WHERE salary>10000;
				
			#需求2：查询job_id不是AD_pres的员工名和工种
				SELECT last_name,job_id FROM employees WHERE job_id<>'AD_PRES';

		2.按逻辑表达式查询
			#需求1：查询工资>=9000 并且工资<=10000的员工工资和姓名
				SELECT salary,last_name FROM employees WHERE salary>=9000 AND salary<=10000;

			#需求2：查询工种编号 不是 st_clerk、sa_rep 并且工资>3000的员工信息
				SELECT * FROM employees WHERE NOT(job_id='ST_CLERK' OR job_id='SA_REP') AND salary>3000;

		3.模糊查询😀
			3.1like关键字：
			#需求1：查询姓名中第一个字符是a的员工信息
				SELECT * FROM employees WHERE last_name LIKE 'a%';

			#需求2：查询邮箱中包含e的信息
				SELECT * FROM employees WHERE email LIKE '%e%';

			#需求3：查询姓名中第二个字符是a，第四个字符e 的员工信息
				SELECT * FROM employees WHERE last_name LIKE '_a_e%';
				
			#需求4：查询员工编号是2开头，1结尾或2开头，3结尾的员工信息
				SELECT * FROM employees WHERE employee_id LIKE '2%1' OR employee_id LIKE '2%3';

			#需求5：查询姓名中第二个字符是 _ 的员工信息
				SELECT * FROM employees WHERE last_name LIKE '_\_%';
			😀SELECT * FROM employees WHERE last_name LIKE '_$_%' ESCAPE '$';($代表转义字符)
			
			3.2 in关键字
			#需求1：查询部门编号是 30 或50或80或90的员工信息
				SELECT * FROM employees WHERE department_id IN(30,50,80,90);
				#等价于
				SELECT * FROM employees WHERE department_id = 30 OR department_id = 50 OR department_id = 80 OR department_id = 90;

			#需求2：查询工种编号是ST_CLERK或是SA_REP的工种、姓名和工资
				SELECT job_id,last_name,salary
				FROM employees 
				WHERE job_id IN ('ST_CLERK','SA_REP');
				#等价于
				SELECT job_id,last_name,salary
				FROM employees
				WHERE job_id = 'ST_CLERK' OR job_id = 'SA_REP';
				
			3.3 between and
			#需求1：查询员工编号在120到200之间的员工信息
				SELECT * FROM employees WHERE employee_id BETWEEN 120 AND 200;
				#等价于
				SELECT * FROM employees WHERE employee_id>=120 AND employee_id<=200;

			#需求2：查询工资在5000到20000之间的员工姓名和工资
				SELECT last_name,salary FROM employees WHERE salary BETWEEN 5000 AND 20000;

			3.4 is null/is not null
			#需求1：查询没有奖金的员工信息
				SELECT * FROM employees WHERE commission_pct IS NULL;

			#需求2：查询有奖金的员工奖金和总工资
				SELECT commission_pct,salary*12*(1+commission_pct) 总工资
				FROM employees
				WHERE commission_pct IS NOT NULL;

	<=>安全等于:😀
		特点：
			用于判断某个字段值是否等于 null
		
		<=> 与 = 与 is 对比：
					判断普通值			判断null	 	    不足
			<=>			√					√			语义性较差
			=			√					×
			is			×					√
	
		案例：
			#需求1：查询没有奖金的员工信息
				SELECT * FROM employees WHERE commission_pct <=> NULL;

			#需求2：查询工资=24000的员工信息
				SELECT * FROM employees WHERE salary<=>24000;
				
排序查询😀
	语法：😀
		select 查询列表
		from 表名
		【where 条件】
		order by 排序的规则 asc|desc

	特点：
		1.asc 代表升序(默认), desc代表降序
		2.order by 一般来讲，从书写上或执行顺序上都是最后
		3.按单个字段、多个字段、表达式、函数、别名或组合排序
	
	案例：
		#一、按单个字段进行排序
			#需求1：查询员工信息，按工资从低到高排序
				SELECT * FROM employees ORDER BY salary ASC;😀

			#需求2：查询有奖金的员工信息，按奖金率从高到低排序
				SELECT * 
				FROM employees
				WHERE commission_pct IS NOT NULL
				ORDER BY commission_pct DESC;

		#二、按多个字段进行排序
			#需求1：查询员工的工资、姓名、编号，先按工资从高到低，再按姓名从低到高排序
				SELECT salary,last_name,employee_id
				FROM employees 
				ORDER BY salary DESC,last_name ;
				
		#三、按表达式进行排序
			#需求1：查询员工的工资、年薪、姓名，按年薪从高到低排序
				SELECT salary,salary*12*(1+IFNULL(commission_pct,0)) 年薪 ,last_name
				FROM employees
				ORDER BY salary*12*(1+IFNULL(commission_pct,0)) DESC;

		#四、按别名进行排序
			#需求1：查询员工的工资、年薪、姓名，按年薪从高到低排序
				SELECT salary,salary*12*(1+IFNULL(commission_pct,0)) 年薪 ,last_name
				FROM employees
				ORDER BY 年薪 DESC;

		#五、按函数进行排序
			#需求1：按姓名的长度进行从高到低排序
				SELECT last_name,LENGTH(last_name) 长度
				FROM employees
				ORDER BY LENGTH(last_name) DESC;

常见函数😀
	理解：
		相当于方法，①叫什么 ②干什么
		
	分类：😀
		单行函数:
			1.字符函数:
				concat、substr、instr、trim、lpad、rpad、length、replace、upper、lower
				
			2.数学函数
				rand、floor、ceil、round
	
			3.日期函数
				now、curdate、curtime、str_to_date、date_format
				
			4.流程控制函数
				if、case（2种）
				
			5、其他系统函数

		分组函数（聚合函数）:
			1.max
			2.min
			3.avg
			4.sum
			5.count
			语法：😀
				select 函数名(实参列表)  【from 表】;
				注意：
					mysql索引从1开始

	案例：
		#一、单行函数😀
			#1.字符函数
				#upper 变大写
					SELECT UPPER('john');
					SELECT UPPER(last_name) FROM employees;
					
				#lower 变小写
					SELECT LOWER('JohN');
					SELECT LOWER(last_name) FROM employees;
					
				#substr截取子串
					SELECT SUBSTR('张三丰',2);
					SELECT SUBSTR('张三丰',2,1);

				#concat拼接
					SELECT CONCAT('张三丰','郭襄');

				#练习：将姓和名拼接在一起，其中性和名的首字符都大写，其他字符消息
					UPPER(SUBSTR(first_name,1,1))
					LOWER(SUBSTR(first_name,2))
					SELECT CONCAT(UPPER(SUBSTR(first_name,1,1)),
                              		LOWER(SUBSTR(first_name,2)),
                                  	UPPER(SUBSTR(last_name,1,1)),
                                    LOWER(SUBSTR(last_name,2))) 姓名
					FROM employees

				#instr 获取子串在字符串中第一次出现的索引,找不到返回0
					SELECT INSTR('childrdednd','z');

				#练习：查询邮箱不合法的员工信息。不合法：邮箱中不包含@
					SELECT * 
					FROM employees
					WHERE INSTR(email,'@')=0;

				#lpad/rpad 左填充/右填充
					SELECT LPAD('hello',10,'@');
					SELECT RPAD('hello',10,'@');

				#trim 去前后空格/@
					SELECT LENGTH(TRIM('         hel  lo        '));
					SELECT TRIM('@' FROM  '@@@@@@@@好孩@@子@@@@@@@@@@@@@') a;

				#replace替换
					SELECT REPLACE('张三丰和郭襄张三丰张三丰','张三丰','杨过');

			#2.数学函数
				#rand 随机数 0——1之间的小数  [0,1)
					SELECT RAND();
					
				#ceil 向上取整 >=该数的最小整数
					SELECT CEIL(-1.23);
					
				#floor 向下取整 <=该数的最大整数
					SELECT FLOOR(-1.23);

				#round
					SELECT ROUND(1.46);
					SELECT ROUND(1.46,1);
					SELECT ROUND(-1.501);

			#3.日期函数
				#now 获取当前日期+时间
					SELECT NOW();

				#curdate 获取当前日期，不包含时间
					SELECT CURDATE();

				#curtime 获取当前时间，不包含日期
					SELECT CURTIME();

				#str_to_date 将字符串解析成日期
					SELECT STR_TO_DATE('1998-3-5','%Y-%c-%d');

				#需求：查询入职日期>'3-5 2014'
					SELECT * FROM employees WHERE hiredate > STR_TO_DATE('3-5 2014','%c-%d %Y');

				#date_format 将日期转换成指定格式字符串，类似于：SimpleDateFormat
#DateTimeFormatter
				#需求：获取员工的姓名和入职日期，形式：xxxx年xx月xx日
					SELECT last_name,DATE_FORMAT(hiredate,'%Y年%m月%d日') 入职日期 
					FROM employees;

			#4.流程控制函数
				#1、if函数，类似于：if else或三目运算符
					SELECT IF(10>9,'哈哈哈','呵呵呵');
					
				#需求1：查询员工的奖金率，如果有奖金，则显示奖金，如果没有，显示无
						SELECT last_name,commission_pct,
						IF(commission_pct IS NOT NULL,commission_pct,'无') 备注
						FROM employees;
						
				#2、case函数，类似于:switch case或多重分支
					#情况1：类似于Java中switch
						switch(变量){
  					 		CASE 常量1：语句1;break;
                       	  	  CASE 常量2：语句2;break;
                          		...
   							DEFAULT:语句n;
						}

					语法：
						CASE 字段或表达式
							WHEN 常量1 THEN 语句1
							WHEN 常量2 THEN 语句2
							...
							ELSE 语句n
							END

					#需求1：查询员工的部门编号和原工资、新工资，如果部门编号是30，则工资显示为原工资的2倍，如果是40，则工资显示为原工资的3倍；
					#如果部门编号是50，则工资显示为原工资的4倍，否则显示成原工资
						SELECT department_id,salary,
							CASE department_id
							WHEN 30 THEN salary*2
							WHEN 40 THEN salary*3
							WHEN 50 THEN salary*4
							ELSE salary
							END  新工资
						FROM employees;

               	 	#情况2：类似于多重if
				   #需求2：查询员工的部门编号和工资和备注，如果工资>20000,备注显示成：A；如果工资>15000,备注显示成：B
				   #如果工资>10000,备注显示成C，否则显示成D
				   SELECT department_id,salary,
						CASE 
						WHEN salary>20000 THEN 'A'
						WHEN salary>15000 THEN 'B'
						WHEN salary>10000 THEN 'C'
						ELSE 'D'
						END 备注
					FROM employees;

		#二、分组函数😀
			#简单查询
				SELECT MAX(salary) 最大值 FROM employees;
				SELECT MIN(salary) 最小值 FROM employees;
				SELECT SUM(salary) 求和 FROM employees;
				SELECT AVG(salary) 平均 FROM employees;
				SELECT COUNT(salary) 工资个数 FROM employees;
				SELECT MAX(salary),MIN(salary) FROM employees;

			#实参类型？
				#1.max/min 实参支持任意类型
					SELECT MAX(last_name) FROM employees;
					SELECT MIN(last_name) FROM employees;
					SELECT MAX(hiredate) FROM employees;

				#2.sum/avg 实参只支持数值型
					SELECT SUM(last_name) FROM employees;
					SELECT AVG(last_name) FROM employees;
					SELECT SUM(hiredate) FROM employees;
					SELECT AVG(hiredate) FROM employees;

				#3.count 实参支持任意类型
					SELECT COUNT(last_name) FROM employees;
					SELECT COUNT(hiredate) FROM employees;

			#统计时，都忽略null值
				SELECT MAX(commission_pct) 最大值 FROM employees;
				SELECT MIN(commission_pct) 最小值 FROM employees;
				SELECT SUM(commission_pct) 求和 FROM employees;
				SELECT AVG(commission_pct) 平均,SUM(commission_pct)/35,SUM(commission_pct)/107 FROM employees;
				SELECT COUNT(commission_pct) 奖金个数 FROM employees;

			#关于count使用
				SELECT COUNT(commissioon_pct) FROM employees;
				SELECT COUNT(*) FROM employees;【推荐使用】
				SELECT COUNT('john') FROM employees;
				SELECT COUNT(DISTINCT department_id) FROM employees;【推荐使用】
		
分组查询😀
	语法：😀
		select 查询列表
		from 表
		where 条件表达式
		group by 分组列表
		having 条件表达式
		order by 排序列表
		
	特点：
		1.查询列表是分组函数、被分组的字段，或二者组合
		2.分组查询的筛选有两类：
			分组前筛选和分组后筛选
	对比：
					针对结果集	     使用关键字		 位置
		分组前筛选	原始表			   where		   group by前面
		分组后筛选	分组后的结果集		having			group by后面
	
		where——group by——having
		分组函数做条件的话，放在having子句中
		如果条件既可以放在where子句又可以放在having子句，建议放在where子句
	案例：
		3、可以按单个字段或多个字段进行分组。
		#引入：查询每个部门的平均工资
			SELECT AVG(salary) 平均工资,department_id
			FROM employees
			GROUP BY department_id;

		#1.简单的分组
			#案例1：查询每个工种的员工平均工资
				SELECT AVG(salary) 平均工资,job_id
				FROM employees
				GROUP BY job_id;

			#案例2：查询每个位置的部门个数
				SELECT COUNT(*),location_id FROM departments
				GROUP BY location_id;

		#可以实现分组前的筛选
			#案例1：查询邮箱中包含a字符的 每个部门的最高工资
				SELECT MAX(salary) 最高工资,department_id
				FROM employees
				WHERE email LIKE '%a%'
				GROUP BY department_id;

			#案例2：查询有奖金的每个领导手下员工的平均工资
				SELECT AVG(salary) 平均工资,manager_id 领导
				FROM employees
				WHERE commission_pct IS NOT NULL
				GROUP BY manager_id;

		#分组后筛选
			#案例1：查询哪个部门的员工个数>5
				#①先查询每个部门的员工个数是多少
					SELECT COUNT(*),department_id
					FROM employees
					GROUP BY department_id
				#②在①结果基础上筛选个数>5的
					SELECT COUNT(*),department_id
					FROM employees
					GROUP BY department_id
					HAVING COUNT(*)>5;

			#案例2：每个工种有奖金的员工的最高工资>12000的工种编号和最高工资
				#①先查询每个工种有奖金的员工的最高工资
					SELECT MAX(salary) 最高工资,job_id
					FROM employees
					WHERE commission_pct IS NOT NULL
					GROUP BY job_id
				#②在 刚才①基础上筛选最高工资>12000
					SELECT MAX(salary) 最高工资,job_id
					FROM employees
					WHERE commission_pct IS NOT NULL
					GROUP BY job_id
					HAVING 最高工资>12000;

			#案例3：领导编号>102的每个领导手下的最低工资大于5000的领导编号和最低工资
				SELECT manager_id,MIN(salary)
				FROM employees
				WHERE manager_id >102
				GROUP BY manager_id
				HAVING MIN(salary)>5000;

		#添加排序
			#案例：每个工种有奖金的员工的最高工资>6000的工种编号和最高工资,按最高工资升序
				SELECT job_id,MAX(salary) 最高工资
				FROM employees
				WHERE commission_pct IS NOT NULL
				GROUP BY job_id
				HAVING 最高工资>6000
				ORDER BY 最高工资;

		#按多个字段分组
			#案例：查询每个工种每个部门的最低工资,并按最低工资降序
				SELECT MIN(salary),job_id,department_id
				FROM employees
				GROUP BY job_id,department_id
				ORDER BY MIN(salary) DESC;
连接查询😀
	概念：
		查询结果集中涉及到多个表，可以使用多表连接查询，简称连接查询
		
	语法：
		select 字段1，字段2,... from 表1，表2;
		
	笛卡尔积：
		表1 m行，表2 n行，结果 = m * n 行	
		解决办法：
			添加匹配条件

	分类：😀
		1.SQL92语法的连接查询
			内连接：
				等值连接
				非等值连接
				自连接
				
			外连接：mysql不支持
	
		2.SQL99语法的连接查询
			内连接：
				等值连接
				非等值连接
				自连接
				
			外连接：
				左外连接
				右外连接
				全外连接 （mysql不支持）
	案例：😀
		1.SQL92语法的连接查询
			#等值连接😀
				语法：
					select 查询列表
					from 表1 别名1，表2 别名2,...
					where 连接条件
					and 筛选条件
					group by 分组列表
					having 分组后筛选条件
					order by 排序列表

				特点：
					1.一般多表连接，需要为表起别名
					2.n个表连接的话，需要至少 n-1 个连接条件
					3.等值连接不分主次表，所以 from 后的表没有顺序要求

			#1.简单两表查询
				#案例1：查询女神名和对应的男神名
				SELECT NAME,boyName
				FROM beauty,boys
				WHERE boyfriend_id=boys.id;

				#案例2：查询员工名和对应的部门名
				SELECT last_name,department_name
				FROM employees e,departments d
				WHERE e.`department_id`=d.`department_id`;
				
			#2.为表起别名
				#查询员工名、工种号、工种名
				SELECT e.last_name,e.job_id,j.job_title
				FROM jobs j,employees e
				WHERE j.`job_id`=e.`job_id`;

			#3.两个表的顺序是否可以调换
				#查询员工名、工种号、工种名
				SELECT e.last_name,e.job_id,j.job_title
				FROM employees e,jobs j
				WHERE j.`job_id`=e.`job_id`;

			#4.可以加筛选
				#查询有奖金的员工名、部门名
				SELECT last_name,department_name
				FROM employees e,departments d
				WHERE e.`department_id`=d.`department_id`
				AND commission_pct IS NOT NULL;

				#查询城市名中第二个字符为o的部门名和城市名
				SELECT department_name,city
				FROM departments d,locations l
				WHERE d.`location_id`=l.`location_id`
				AND city LIKE '_o%';

			#5.可以加分组
				#案例1：查询每个城市的部门个数
				SELECT COUNT(*) 个数,city
				FROM departments d,locations l
				WHERE d.`location_id`=l.`location_id`
				GROUP BY city
				HAVING 个数>10;

				#案例2：查询有奖金的每个部门的部门名和部门的领导编号和该部门的最低工资
				SELECT d.`manager_id`,MIN(salary),d.`department_id`
				FROM departments d,employees e
				WHERE d.`department_id`=e.`department_id`
				GROUP BY d.`department_id`

			#6.可以加排序
				#查询每个工种的员工个数和工种名，并按个数排序
				SELECT job_title,COUNT(*) 员工个数
				FROM jobs j,employees e
				WHERE j.job_id = e.`job_id`
				GROUP BY job_title
				ORDER BY 员工个数 DESC;

			#7、可以实现三表连接
				#案例：查询员工名、部门名和所在的城市
				SELECT last_name,department_name,city
				FROM employees e,departments d,locations l
				WHERE e.`department_id`=d.`department_id`
				AND d.`location_id`=l.`location_id`;
				
			#非等值连接😀
				语法：
					select 查询列表
					from 表1 别名1，表2 别名2，...
					where 连接条件
					group by 分组
					having 筛选条件
					order by 排序

				特点：
					连接条件为非等值判断

				#案例1：查询员工的工资和工资级别
					SELECT employee_id,salary,grade_level
					FROM employees e,job_grades g
					WHERE e.`salary` BETWEEN g.`lowest_sal` AND g.`highest_sal`;

			#自连接😀
				特点：
					一张表当做多张表去使用

				#案例1：查询员工名和它的上级领导名
					SELECT e.employee_id,e.last_name,e.manager_id,m.`last_name`
					FROM employees e,employees m
					WHERE e.`manager_id` = m.`employee_id`;

		2.SQL99语法的连接查询😀
			#内连接查询😀
				语法：
					select 查询列表
					from 表1 别名1
					inner|outer join 表2 别名2
					on 连接条件
					where  筛选条件
					group by 分组
					having 分组后筛选
					order By 排序
					
				特点：
					连接条件和筛选条件进行了分离，提高了语义性

			#等值连接😀
				特点：
					①n表连接，至少需要 n-1 个连接条件
					②表没有主从之分
					③inner 可以省略

				#案例1.查询员工名、部门名
					SELECT last_name,department_name
					FROM employees e
					JOIN departments d
					ON e.`department_id`=d.`department_id`;

				#案例2.查询名字中包含e的员工名和工种名
					SELECT last_name,job_title
					FROM employees e
					INNER JOIN jobs j
					ON e.`job_id` = j.`job_id`
					WHERE last_name LIKE '%e%';

				#案例3： 查询部门个数>3的城市名和部门个数【添加分组+分组后筛选】
					#①查询每个城市的部门个数
					SELECT COUNT(*) 部门个数,city
					FROM departments d
					INNER JOIN locations l
					ON d.`location_id`=l.`location_id`
					GROUP BY city;
					#②在刚才①基础上进行筛选
					SELECT COUNT(*) 部门个数,city
					FROM departments d
					INNER JOIN locations l
					ON d.`location_id`=l.`location_id`
					GROUP BY city
					HAVING 部门个数>3;

				#案例4：查询哪个部门的员工个数>3的部门名和员工个数，并按员工个数降序（添加排序）
					#①查询每个部门的员工个数、部门名
					SELECT COUNT(*) 员工个数,department_name
					FROM departments d
					INNER JOIN employees e
					ON e.`department_id`=d.`department_id`
					GROUP BY department_name
					#②在①结果上筛选，并排序
                      SELECT COUNT(*) 员工个数,department_name
                      FROM departments d
                      INNER JOIN employees e
                      ON e.`department_id`=d.`department_id`
                      GROUP BY department_name
                      HAVING 员工个数>3
                      ORDER BY 员工个数 DESC;

				#案例5:查询员工名、部门名、工种名，并按部门名降序【三表连接】
					SELECT last_name,department_name,job_title
					FROM employees e
					INNER JOIN departments d  ON e.`department_id`=d.`department_id`
					INNER JOIN jobs j ON e.`job_id`=j.`job_id`
					ORDER BY department_name DESC;

			#非等值连接😀
				#案例1：查询有奖金的每个员工的工资级别
				SELECT employee_id,last_name,salary,commission_pct,grade_level
				FROM employees e
				JOIN job_grades g 
				ON e.`salary` BETWEEN g.`lowest_sal` AND g.`highest_sal`
				WHERE commission_pct IS NOT NULL;
				GROUP BY grade_level;

			#自连接😀
				#案例1：查询部门号>100的员工名和他的领导名
				SELECT e.last_name,e.department_id,m.last_name
				FROM employees e
				JOIN employees m
				ON e.`manager_id`=m.`employee_id`
				WHERE e.`department_id`>100;

			#外连接查询😀
				语法：
					select 查询列表
					from 表1 别名
					left|right outer join 表2 别名
					on 连接条件
					
				分类：
					左外连接：
						左边表是主表
						查询结果：
						左边的表的全部记录（交集部分+左表有，但右表没有）
					右外连接：
						右边的表是主表
						查询结果：
						右边的表的全部记录（交集部分+右表有，但左表没有）
					全外连接：mysql 不支持，full outer join on
					
				特点：
					1.查询结果 = 主表的全部记录（交集部分+主表有，但从表没有）
					2.区分主从表
					3.outer可以省略
					
				#案例1.查询所有女神的男朋友信息
				SELECT b.name,b.boyfriend_id,bo.*
				FROM beauty b 
				LEFT OUTER JOIN boys bo 
				ON b.`boyfriend_id`=bo.`id`;

				#案例2.查询没有男朋友的女神名
				SELECT b.name
				FROM beauty b 
				LEFT OUTER JOIN boys bo 
				ON b.`boyfriend_id`=bo.`id`
				WHERE bo.`id` IS NULL;

				#案例3.查询哪个部门没有员工
				SELECT d.`department_name`,d.`department_id`
				FROM employees e
				RIGHT JOIN departments d 
				ON e.`department_id` = d.`department_id`
				WHERE e.`employee_id` IS NULL;

子查询😀
	概念：
		出现在其他语句内部的查询，称为子查询
			其他语句可以是：
				insert、update、delete、select
		如果其他语句是select，或里面嵌套查询语句的select语句，称为主查询

	按位置分类：
		1.select后面
		2.from后面
		3.where或having后面（条件）😀
		4.exists后面(相关子查询)
		
	按结果集行数、列数分类：
		1.标量子查询（一行一列）😀
		2.多行子查询（多行一列）😀
		3.列子查询（一行多列）
		4.表子查询（多行多列）
		
	子查询放在where或having后面，特点：
		1.子查询一般放在小括号内
		2.子查询先于主查询执行
		3.子查询一般搭配着单行或多行子查询操作符使用 😀
			单行：> < >= <= = <>
			多行：in / not in、any、all

	#标量子查询（单行子查询）😀
		#1.谁的工资比 Abel 高
			#①先查询Abel的工资
			SELECT salary FROM employees WHERE last_name = 'Abel'
			#②查询员工的信息，salary>①
			SELECT * FROM employees WHERE salary>(
				SELECT salary FROM employees WHERE last_name = 'Abel'
			);
			
		#2.返回job_id与141号员工相同，salary比143号员工多的员工姓名，job_id 和工资
			#①查询141员工的job_id
			SELECT job_id 
			FROM employees
			WHERE employee_id = 141
			#②查询143号员工的salary
			SELECT salary 
			FROM employees
			WHERE employee_id = 143
			#③查询job_id = ①，并且 salary>②
			SELECT last_name,job_id,salary
			FROM employees
			WHERE job_id = (
				SELECT job_id 
				FROM employees
				WHERE employee_id = 141
			) AND salary > (
				SELECT salary 
				FROM employees
                  WHERE employee_id = 143
            );

		#3.返回工资最少的员工的last_name,job_id和salary
			#①查询最低工资
			SELECT MIN(salary) FROM employees;
			#②查询谁的工资=①
			SELECT last_name,job_id,salary
			FROM employees
			WHERE salary = (
				SELECT MIN(salary)
				FROM employees
			);

		#4.查询最低工资大于50号部门最低工资的部门id和其最低工资
			#①查询50号部门的最低工资
			SELECT MIN(salary)
			FROM employees
			WHERE department_id = 50
			#②查询每个部门的最低工资，并且筛选看哪个部门的最低工资>①
			SELECT MIN(salary) 最低工资,department_id
			FROM employees
			GROUP BY department_id
			HAVING 最低工资>(
				SELECT MIN(salary)
				FROM employees
				WHERE department_id = 50
			);

	#多行子查询（一列多行）😀
		#1.返回location_id是1400或1700的部门中的所有员工姓名
			#①查询location_id是1400或1700的部门编号
			SELECT DISTINCT department_id 
			FROM departments
			WHERE location_id IN(1400,1700)
			#②查询部门编号是①中的一个的所有员工姓名
			SELECT last_name
			FROM employees
			WHERE department_id IN(
				SELECT DISTINCT department_id 
				FROM departments
				WHERE location_id IN(1400,1700)
			);

		#2.返回其它部门中比job_id为‘IT_PROG’部门任意一工资低的员工的员工号、姓名、job_id 以及salary
  			#①查询job_id 为‘IT_PROG’部门的工资
  			SELECT DISTINCT salary
  			FROM employees
  			WHERE job_id = 'IT_PROG'
  			#②查询其他部门的工资<any① 的信息
  			SELECT last_name,employee_id,job_id,salary
  			FROM employees
 			WHERE salary<ANY(
	 			SELECT DISTINCT salary
	  			FROM employees
	  			WHERE job_id = 'IT_PROG'
  			) AND job_id<>'IT_PROG';
  
 		 #3.返回其它部门中比job_id为‘IT_PROG’部门所有工资都低的员工的员工号、姓名、job_id 以及salary
   			SELECT last_name,employee_id,job_id,salary
  			FROM employees
 			WHERE salary<ALL(
	  			SELECT DISTINCT salary
	  			FROM employees
	  			WHERE job_id = 'IT_PROG'
  			) AND job_id<>'IT_PROG';

	分页查询 😀
		应用场景：
			当前台需要分页显示条目时，需要向数据库服务器提交请求查询对应条目的数据
	
		语法：
			select 查询列表
			from 表
			【inner join 表 on 连接条件
			where 条件
			group by 分组
			having 筛选
			order by 排序】
			limit 起始索引,条目数;()

		特点：😀
			1.起始条目索引，可以省略，默认第一条
			2.第一条的索引: 0
		
		案例：
			#需求1：查询前五条
				SELECT * FROM employees LIMIT 5;
				
			#需求2：查询第10——20条
				SELECT * FROM employees LIMIT 9,11;
				
			#需求3：查询工资最高的前五名
				SELECT * FROM employees ORDER BY salary DESC LIMIT 5;

	联合查询/合并查询😀
		语法：😀
			select 查询列表 from 表 where 条件 union
			select 查询列表 from 表 where 条件 union
				....
			select 查询列表 from 表 where 条件 
	
		应用场景：
			1、表格：Chinese/American
				Chinese:
					姓名	年龄	性别
					张三丰	12	男
				American:
					name   age	gender
					john   12	boy
		
				select 姓名,年龄，性别 from chinese union
				select name,age,gender from american;
					张三丰	12	男
					john  12   boy

			2、查询多个条件下的数据：
				查询姓名包含e的，或工资>10000或邮箱不为null或奖金>0.3的或部门编号>的员工姓名、工资
				SELECT last_name,salary FROM employees WHERE last_name LIKE '%e%' 				  			UNION
				SELECT last_name,salary FROM employees WHERE salary>10000 
				UNION
				SELECT last_name,salary FROM employees WHERE email IS NOT NULL                 					UNION
				SELECT last_name,salary FROM employees WHERE commission_pct >0.3                    	 		UNION
				SELECT last_name,salary FROM employees WHERE department_id>90
		
		特点：😀
			1.要求多条待合并的查询语句的查询列表的个数和类型最好一致
			2.union 默认实现的是去重查询；如果想包含重复项，可以使用 union all
```

###### DML语言😀

```mysql
DML:
	Data Manipulate Language 数据操纵语言
	insert / update / delete
	
特点：
	1.插入和删除时，都是针对行数据的
	2.字符型和日期型数据，要求使用单引号；

分类：
	1.插入数据（insert）😀
		形式1：插入单行
			语法：😀
				insert into 表名(字段名,字段名,...) values / value(值,值,...);

			特点：
				1.字段和值要一一对应，类型一致或兼容
				2.字段个数和值个数必须一致
				3.字段的顺序可以调换，但值顺序也要跟着调换
				4.可以省略字段名，默认所有字段，而且顺序和字段存储顺序一致
				5.可以为空或默认的字段，不用手动插入值，使用 null 或 default 关键字填充即可,或字段和值都不写
			
			案例：
				#1.插入一行简单数据
					INSERT INTO beauty(id,NAME,sex,borndate,phone,boyfriend_id)
					VALUE(30,'赵丽颖','女','1986-1-1','110',5);

				#2.字段可以调换顺序
					INSERT INTO beauty(id,sex,borndate,phone,boyfriend_id,NAME)
					VALUES(21,'女','1983-1-1','120',4,'高圆圆');

				#3.可以为空或默认值的字段可以不用手动设置值
					#方式一：直接字段和值都不写
					INSERT INTO beauty(id,phone,NAME)
					VALUES(22,'120','何洁');
					#方式二：字段写上，值使用null或default关键字
					INSERT INTO beauty(id,sex,borndate,phone,boyfriend_id,NAME)
					VALUES(23,DEFAULT,DEFAULT,'120',NULL,'李宇春');

				#4.字段名可以省略，默认所有字段
					INSERT INTO beauty
					VALUES(25,'欧阳娜娜',NULL,'1998-1-1','111',9);
					
		形式2：插入多行数据😀
			语法：
				insert into 表名(字段名，字段名,...) 
				values (值，值,...),(值，值,...),(值，值,...),(值，值,...);
				
			案例：
				INSERT INTO beauty(id,NAME,sex,phone)
				VALUES (31,'lucy','女','123'),
				(32,'lily','女','123'),
				(33,'rose','女','123'),
				(34,'jerry','女','123');

	2.修改语句（update)😀
		形式1.单表修改
			语法：
				update 表名
				set 字段名 = 新值,字段名 = 新值
				where 条件;
				
			案例：
				UPDATE beauty SET NAME = '马思纯' WHERE id = 31;
                
				UPDATE beauty SET sex='男' WHERE boyFriend_id = 9 AND phone LIKE '11%';

				UPDATE beauty SET sex='女',phone = '13211110000' WHERE boyFriend_id = 9 ;

		形式2.多表修改
			语法：
				update 表1,表2
				set 字段名=新值,字段名=新值
				where 连接条件
				and 筛选条件;
			
			案例：
				#需求：修改男神名为黄晓明的魅力值为500，并且女朋友的电话：189
				UPDATE beauty b,boys bo
				SET usercp = 500,phone = '189'
				WHERE b.`boyfriend_id`=bo.`id`
				AND bo.`boyName`='黄晓明';

	3.删除数据😀
		delete
			#形式1:单表删除
				语法：
					delete from 表名 where 条件	
				
			#形式2：多表级联删除
				语法：
					delete 别名1,别名2 
					from 表名 别名1,表名 别名2 
					where 连接条件
					and 筛选条件
					
				案例：
					#删除鹿晗的女朋友信息
					DELETE b
					FROM beauty b,boys bo
					WHERE b.boyfriend_id = bo.id
					AND bo.boyname='鹿晗';
					
		truncate
			语法：
				truncate table 表名;
			
			案例：
				#需求1：删除表admin中的所有数据
					TRUNCATE TABLE admin;

		delete 与 truncate 对比：
			1.delete 语句可以添加 WHERE 条件，实现有条件的删除，TRUNCATE 语句不可以添加WHERE 条件，不可以实现有条件删除
			2.truncate 效率较高
			3.delete 删除带自增长列的表，再次插入时，自增长列从断点处继续增长，TRUNCATE 删除带自增长列的表，再次插入时，自增长列从1开始增长
			4.delete 语句，可以返回受影响行数，TRUNCATE 语句，没有返回受影响行数
				DELETE FROM admin;
				TRUNCATE TABLE admin;
```

###### DDL语句😀

```mysql
DDL：
	Data Define Language 数据定义语言
	create 创建 / alter 修改 / drop 删除

分类：😀
	1.库的管理：
		#1.库的创建：
			CREATE DATABASE IF NOT EXISTS 库名;
			
		#2.库的删除:
			DROP DATABASE IF EXISTS 库名;

	2.表的管理
		#1.表的创建 
			create table 【IF NOT EXISTS 】表名(
   			列名 数据类型 【约束】,
   			列名 数据类型 【约束】,
   				...
   			列名 数据类型 【约束】);

MySQL数据类型：😀
	整型：
		int / tinyint / smallint / mediumint/ bigint
		
    浮点型：😀
  		float(m,n) / double(m,n) 
  		m：整数部位 + 小数部位总长度;
  		n：小数部位长度
  		
	字符型：😀
	char(m) / varchar(m)  
		m：最多的字符个数
			char： 默认为 1，可以省略，
			varchar： 不可以省略
			
	日期型:😀
		datetime / date/ time / timestamp（时间戳）
		
		datetime 与 timestamp 对比：
						日期范围		字节空间	移植性					
			datetime	1900-某个时间	 	8		不会有变化
			timestamp	1970-2038年		  4		   时区 / 服务器版本不同有所变化  
		
表的修改
	语法：😀
		alter table 表名 add|modify|drop|change column 字段名 【新字段类型 新字段约束】
		
	案例：
		#①修改表名
			ALTER TABLE students RENAME TO stuinfo;

		#②添加字段
			ALTER TABLE stuinfo ADD COLUMN borndate TIMESTAMP ;

		#③修改字段数据类型或约束
			ALTER TABLE stuinfo MODIFY COLUMN id VARCHAR(10);

		#④修改字段名
			ALTER TABLE stuinfo CHANGE COLUMN id stuNo VARCHAR(10);

		#⑤删除字段
			ALTER TABLE stuinfo DROP COLUMN email;

表的删除😀
	语法：
		DROP TABLE IF EXISTS 表名;
		
表的复制😀
	形式1：仅仅复制表的结构
		CREATE TABLE person LIKE students;

	形式2：复制表的结构 + 内容
		CREATE TABLE people SELECT * FROM students;
		
		CREATE TABLE people
		SELECT id,NAME,gender
		FROM students
		WHERE id <= 3;

自增长列😀（AUTO_INCREMEN）
	概念：
		设置为自增长列的字段的值，不用手动插入，可以实现自增长。默认从 1 开始，步长为 1
	
	特点：
		1.一个表至多有一个自增长列
		2.自增长列类型:数值型
		3.自增长列必须添加在设置了主键、唯一键或外键字段上
	
	案例：
		#创建表时，添加自增长列😀
			CREATE TABLE major(
				id INT PRIMARY KEY AUTO_INCREMENT,
				name VARCHAR(20)
			);

		#修改表时，添加或删除自增长列
			ALTER TABLE major MODIFY COLUMN id INT AUTO_INCREMENT;
```

###### 常见约束😀

```mysql
理解：
	用于限制某字段的值，为了保证数据一致性或完整性

六大约束：😀
	NOT NULL 非空：
		用于限定被修饰字段不可以为空
		
	DEFAULT 默认:
		用于限定被修饰的字段，不插入值时，有默认值
		
	PRIMARY KEY 主键：😀
		用于限定被修饰的字段值是唯一的，不可重复
        
		特点：
			1.不可以为空
			2.一个表至多有一个主键，建议每个表都有一个主键
		
	UNIQUE 唯一：
		用于限定被修饰字段值是唯一的，不可重复的
		
		特点：
		1.可以为空
		2.一个表中可以有多个唯一键
		
	CHECK 检查：
		用于限定被修饰字段值必须符合定义的条件
		check(条件) mysql不支持，但不会报错
		
	FOREIGN KEY 外键：
		用于限定两个表的关系
		特点：
		1.在从表中添加外键
		2.从表中的关联列来自于主表的关联列

分类：😀
	列级约束：
		NOT NULL,
		DEFAULT,
		UNIQUE,
		PRIMARY KEY ,
		CHECK
	表级约束:
		UNIQUE,
		PRIMARY KEY,
		CHECK,
		FOREIGN KEY
	
列级约束 与 表级约束对比：
				位置		能否起名	支持约束类型				
	列级约束	列的后面	不能		 NOT NULL,DEFAULT,UNIQUE,PRIMARY KEY ,CHECK
	表级约束	所有列后面   能		 UNIQUE,PRIAMRY KEY,CHECK,FOREIGN KEY




语法：
	#创建表时添加约束😀
		create Table 表名(
			字段名 数据类型 列级约束,
			字段名 数据类型 列级约束,
				...
			字段名 数据类型 列级约束,
			表级约束
		)
		
		案例：
			#1：创建stuinfo表
			CREATE TABLE stuinfo(
				stuid INT PRIMARY KEY,
				stuname VARCHAR(20) NOT NULL,
				gender CHAR(1) DEFAULT '男',
				seat INT NOT NULL UNIQUE,
				age INT CHECK(age BETWEEN 0 AND 120),
				majorid INT NOT NULL,
				CONSTRAINT fk_stuinfo_major FOREIGN KEY (majorid) REFERENCES major(id)
			);

	#修改表时添加约束（了解）
		案例：
			CREATE TABLE stuinfo(
				stuid INT ,
				stuname VARCHAR(20),
				gender CHAR(1),
				seat INT ,
				age INT ,
				majorid INT 
			);	
			#1.添加非空
			ALTER TABLE stuinfo MODIFY COLUMN stuname VARCHAR(20) NOT NULL;

			#2.添加默认
			ALTER TABLE stuinfo MODIFY COLUMN gender CHAR(1) DEFAULT '男';

			#3.添加主键
			ALTER TABLE stuinfo MODIFY COLUMN stuid INT PRIMARY KEY;

			#4.添加唯一
			ALTER TABLE stuinfo MODIFY COLUMN seat INT UNIQUE;
			
			#5.添加外键
			ALTER TABLE stuinfo ADD CONSTRAINT fk_stu_major FOREIGN KEY(majorid) REFERENCES major(id);

	#修改表时删除约束（了解）
		案例：
			#1.删除非空
			ALTER TABLE stuinfo MODIFY COLUMN stuname VARCHAR(20) NULL;
			
			#2.删除默认
			ALTER TABLE stuinfo MODIFY COLUMN gender CHAR(1);

			#3.删除主键😀
			ALTER TABLE stuinfo MODIFY COLUMN stuid INT ;#不管用
			ALTER TABLE stuinfo DROP PRIMARY KEY;

			#4.删除唯一😀
			ALTER TABLE stuinfo MODIFY COLUMN seat INT ;#不管用
			ALTER TABLE stuinfo DROP INDEX seat;

			#5.删除外键
			ALTER TABLE stuinfo DROP FOREIGN KEY fk_stu_major;
```

###### 事务😀

```mysql
理解：
	一条或多条 sql 语句组成单元

四大特性：ACID😀
	原子性：
		一个事务是不可再分割单元，要么一起执行，要么一起失败
	一致性：
		一个事务从一种状态切换到另一种状态，数据必须保持一致
	隔离性：
		一个事务执行时，不应该受其他事务干扰
	持久性：
		一个事务一旦 commit，将是永久性的
	
事务分类：
	隐式事务：
		事务没有明显的开启和结束标记。如：insert、update、delete、select 语句
	显式事务：
		事务具有明显的开启和结束标记
		
使用步骤：😀
	0.取消 insert、update、delete、select 自动提交功能
	1.开启事务
	2.编写事务中 1 条或多条 SQL 语句
	3.结束事务：
		commit 提交 或 ROLLBACK 回滚

案例：
	#事务的使用：
		#0、取消insert、update、delete、select的自动提交功能
			SET autocommit = 0;
		
		#1、开启事务
			START TRANSACTION;
			
		#2、编写事务中使用到的1条或多条SQL语句
			UPDATE account SET balance = 5000 WHERE username = '张三丰';
			#意外
			UPDATE account SET balance = 15000 WHERE username = '灭绝';
	
		#3、结束事务：根据需要提交或回滚
			#commit;#提交事务
				ROLLBACK;#回滚事务
```

