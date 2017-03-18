- ## Day1
```php
//php配置(apache)

1，httpd.conf 中添加
PHPIniDir "php语言包所在的目录"
2，站点的核心：
            1，ServerName 站点名称
            2，DocumentRoot 站点真实目录
3，目录访问权限：
    <Directory "要设置权限的物理路径">
        Options Index #设置目录可显示“文件列表”
        Order  Deny,Allow #先拒绝后允许或先允许后拒绝，不管哪个顺序，都是是后者覆盖前者
        Allow  from  All
 
        #在文件夹中设定权限
        AllowOverride  all
        
    </Directory>
4，分布式访问式权限
    目录访问权限中的“分布式权限”：
        一个站点的任何一个文件夹，都可以对其进行“单独权限设置”：
            1，需要在该文件夹中放入一个特殊名字的文件：  .htaccess
            2，该文件夹的内容，几乎可以跟Directory中的设置一样
            3，该文件中的设置，优先于Directory中的设置，即如果有同样设置项但值不同，以.htaccess中的为准；
            4，.htaccess中的设置项，无需重启apache，就可以立即生效。
5，多站点配置：
    1，在http.conf中，打开虚拟主机配置文件：apache安装位置/conf/extra/httpd-vhosts.conf
    2，格式：
        <VirtualHost>
        ServerName ....
        DocumentRoot  .....
        <Directory  .....>
         
        </Directory>
        </VirtualHost>
    3，ServerAlias  别名1  别名2 写在ServerName并列的位置。

```

- ## Day2
```php
1,Php 书写短格式，在php.ini中打开short_open_tag = ON;
2,Php 书写特性
        1，变量区分大小写
        2，常量通常也区分，可设置不区分
        3，函数名，（if for return ...）
        4, 分号 结束
3，变量
    1，值传递
        $ver1 = 1; $ver2 = $ver1; 
    2，引用传递
        $ver1 = 1; $ver2 = & $ver1;
    3，可变变量
        $ver1 = "ver2";
        $ver2 = 10;
        echo $$ver2;
    4, 预定义变量：
        $_GET;$_POST;$_REQUSET;$_SERVER;_GLOBALS
        1，均为数组
        2，系统定义与维护
        3，超全局作用域
        4，不同情景具有不同的值
        
            :$_POST;$_GET;表单提交 
                //提交get表单有 5种形式；
                1,  <from action = "xx.php method = "get">
                        <input type = "text" name = "data1"/>
                        <input type = "text" name = "data2"/>
                        <input type = "submit name = "submit"/>
                    </from>
                2, <a href = "xxx.php?data1 = data1 & data2 = data2">链接传递</a>    
                3,  <script>
                        location.href = "xxx.php?data1=data1 & data2 = data2"
                    </script>
                4, <script>
                        location.assign = "xxx.php?data1=data1 & data2 = data2"
                    </script>
                5,
                    //header("location:xxx.php")
                    //header("location:xxx.php? data1 = "data1" & data2 = "data2")
            :$_REQUEST;
                为$_POST,$_GET合集:如果变量名相同时，后者覆盖前者
                
            :$_SERVER;
                1,$_SERVER['REMOTE_ADDR']:获取访问者的IP地址
                2,$_SERVER['SERVER_ADDR']:获取访问者的ip地址
                3,$_SERVER['SERVER_NAME']:获取服务器NAME(servername)
                4,$_SERVER['DOCUMENT_ROOT'];获取站点的真实物理地址，其实就是站点设置中的documentroot

                5,$_SERVER['PHP_SELF'];获取当前网页地址
                6,$_SERVER['SCRIPT_FILENAME'];获取当前网页地址物理路径
                7,$_SERVER['QUERY_STRING'];获取当前网页地址中的所有get数据
            :$_GLOBALS:全局变量
            
    4，常量：常量相对于变量来说，其中储存的数据不会改变的标识符。
            
            1,define("VERSION","1.0")
            2,const version = "1.0"
            
            //取值
            $a = VERSION;  $a = constant("VERSION"); 
            
            区别:
            
                1，使用形式不同。
                2，可变程度不同（不可改变和销毁）
                3，全局作用域
                4，只能储存标量类型(bool,float,int,string)
                
            判断:
            
                1，defined("VERSION") 是否定义
            
            预定义常量:
                M_PI:圆周率的常量值
                PHP_OS:php运行所在的操作系统
                PHP_VERSION:版本号
                PHP_INT_MAX:最大的整数值
                PHP_EOL:换行符
            魔术变量:
                __FILE__    //当前文件的完整路径
                __DIR__     //当前文件所在的目录
                __LINE__    //当前文件的行号

    5,数据类型:
        
        1,基本类型
            
            整数类型:int.integer
            浮点数类型:float
            字符串类型:string
            布尔类型:bool,boolean
        2,复合类型
            
            数组:array
            对象:object
        3，特殊类型
            
            空类型:null
            资源类型resource
            
        4，整数类型
            $v = 123;   //10 dec
            $v = 0123;  //8 oct
            $v = 0x123; //16 hex
            
            //十进制转化：
                decbin(),decoct(),dechex()  // 2,8 16
        5, 浮点
            //精度为3位比较
            if (round($v/3 * 1000) == round(2.7*1000)) { };
        6，字符串
            $str = <<< "a" Hello World "a"; 
            
            •	var_dump()：用于输出变量的“完整信息”，几乎只用于调试代码。
            •	getType($变量名)：获取该变量的类型名字，返回的是一个表示该类型名字的字符串，比如：“string”，“bool”，“double”，“int”
            •	setType($变量名，“目标类型”)：将该变量强制改变为目标类型；
            •	isset(), empty(), unset();
            
            •   比较 "=="(模糊比较) "==="(精确比较)
            



```
- ## Day3
```php
1，运算符
    
    1，逻辑运算  &&(与), ||(或), !(非)
    2, 字符串拼接 . '将两个字符串连接并类型转换'
    3，赋值运算符 : '+=' ,'-=','*'
2,条件运算
    1, Bool ?  v2 : v3;
3,位运算符
    1,'&'(位与) '|'(位或) '~'(位取反) '^'(位异或) '<<'(左移动)
    
4,原码，反码，补码，
      
      '反码':  正数的反码是起原码本身，负数的反码是
      其符号位不变，其它位取反
      '补码':  正数等于本身，负数：符号位不变，其它位取反后加＋1
```
- ## Day6
```php
    1,函数
    
        1，参数:
        
            1: func_get_args();//获取实参数据列表，成为一个数组
            2: func_get_arg($i);//获取第$i个实参数据，$i从0开始算起；
            3：func_num_args();//获取实参的数量（个数）
            
        2,匿名函数:
            
            1;
            $func1 = function($str):String{
                
                echo "匿名函数";
                return strtoupper($str);
            }
            
            $func1("Hello");
            
            2:
            function func1($x,$y,$z):int {
                
                retrun $x + $y + $z($x + $y);
            }
            $f1 = function($v1,$v2):int {
                
                return $v1 + $v2;
            }
            func1(1,2,$f1(1,2));
        3,作用域：
            1,要点
                1，全局范围不能访问局部变量
                2，局部范围不能访问全局变量；
                3，函数内部的变量（局部变量），通常在函数调用执行结束后，被“销毁”。
                4，局部静态变量，在函数调用结束后不被销毁；
            2，局部操作全局变量
            
                1，使用global关键字实现 :function(){ global $v1;
                    $v1 = 66;
                }
                2，使用$GLOBALS超全局变量来实现 function() {
                    $GLOBAILS['v1'] = 66;
                }
            3,函数相关的系统函数操作
                • function_exists()：判断函数是否被定义过。其中使用的参数为“函数名”
        4,其他常用系统函数:
            • 字符串函数：
                1: 输出与格式化：echo , print, printf, print_r, var_dump.
                2: 字符串去除与填充：trim, ltrim, rtrim, str_pad
                3: 字符串连接与分割：implode, join， explode, str_split
                4: 字符串截取：substr, strchr, strrchr,
                5: 字符串替换：str_replace, substr_replace
                6: 字符串长度与位置： strlen, strpos, strrpos,
                7: 字符转换：strtolower, strtoupper, lcfirst, ucfirst, ucwords
                8: 特殊字符处理：nl2br, addslashes, htmlspecialchars, htmlspecialchars_decode,
                
        5.递归函数:
            function factorial($n) {
                if ($n == 1) {
                    return 1;
                }
                return $n * factorial($n - 1);
            }
            
```

- ## Day7

  ```php
  1,数组基础

  	1, each()函数的使用

  		1,foreach($arr as $key=>$value) {

  		}

  		2,while( list($key,$value) = each($arr) ) {

  		}

  		3,each()函数的作用：先取得一个数组的“当前单元”的下标和值（并放入一个数组），然后将指针移到下一个单元。
            
      4,常用数组相关函数
        
        	1，count()，key()，range()，asort()
        	
  ``` 
- ## Day8
```
    1,MYSQL
        `
        1，连接sql
        
            mysql -h 0.0.0.0 -u root  -p 或 mysql --host=服务器地址 --user=用户名 --port=端口 --password
            
        2，数据库的备份和恢复：
        
            1，mysqldump -h 'ip' -u 'name' -p 'databaseName' > '文件名'
            2, mysql  -h localhost  -u root -p 'databaseName' < 文件名'
            
        3,  创建数据库 
        
            create database dbTest charset utf8 collate utf_general_ci;
        4，删除数据库
        
            drop database if exists databaseName;
            
            //修改
                alter database database_name charset utf8
        5,表操作
            1,创建表
                create table table_name111 (
                    id int auto_increment,
                    user_name varchar(20) not null,
                    f1 float,f2 double,f3 time, f4 text,
                    f5 decimal(10,3),
                    
                    primary key(id),
                    unique(user_name)
                );
            2,外键索引
                //创建tab1
                create table class_info (
                
                	id int auto_increment,
                	class_name varchar(20) not null,
                	stu_count float,
                	
                	primary key(id),
                	unique key(class_name)
                	
                );
                
                //创建tab2
                create table student_info (
                
                	id int auto_increment,
                	class_id int,
                
                	user_name varchar(20),
                	email varchar (50),
                	age int,
                
                	primary key(id),
                	unique key(user_name),
                	foreign key (class_id) references class_info(id)
                );
                
                //
                主键约束：形式： primary key ( 字段名);
                含义（作用）：使该设定字段的值可以用于“唯一确定一行数据”，其实就是“主键”的意思。
                 
                唯一约束：形式： unique   key ( 字段名);
                含义（作用）：使该设定字段的值具有“唯一性”，自然也是可区分的。
                 
                外键约束：形式： foreign key ( 字段名)  references  其他表名(对应其他表中的字段名) ;
                含义（作用）：使该设定字段的值，必须在其谁定的对应表中的对应字段中已经有该值了。
                 
                非空约束： 形式： not  null，其实就是设定一个字段时写的那个“not null”属性。
                这个约束只能写在字段属性上；
                 
                默认约束： 形式： default  XX值；其实就是设定一个字段时写的那个“default  默认值”属性
                这个约束只能写在字段属性上；
                 
                检查约束： 形式： check（某种判断语句），比如：
                create  table  tab1 (
                    age  tinyint,
                    check  (age>=0 and age <100) /*这就是检查约束*/
                )
                
            6，常用关键字
                1，表选项就是，创建一个表的时候，对该表的整体设定，主要有如下几个：
                    charset = 要使用的字符编码，
                    engine = 要使用的存储引擎（也叫表类型），
                    auto_increment = 设定当前表的自增长字段的初始值，默认是1
                    comment = ‘该表的一些说明文字’
                    
            7，表操作
                1，修改表
                    1，添加字段：alter table table_name add column all_age int;
                    2，修改字段: alter table tableName change column old_key_word new_key_wrod int;
                    3，删除字段: alter table table_name drop column key_word
                    4，添加普通索引: alter table table_name add key(id_key)
                    5，添加唯一约束:alter table 表名 add unique key (字段名1[，字段名2,...])
                    6，添加主键索引(约束)：alter table 表名 add primary key (字段名1[，字段名2,...])；
                    7，修改表明:alter  table  旧表名   rename  [to] 新表名；
                    8，删除表：drop  table  【if  exists】 表名；
                2,
                    • 显示当前数据库中的所有表: show tables；
                    • 显示某表的结构: desc 表名； 或：describe 表名；
                    • 显示某表的创建语句：show create table 表名；
                    • 重命名表：rename table 旧表名 to 新表名；
                    • 从已有表复制表结构：create table [if not exists] 新表名 like 原表名;
                3,
                    扩展php中操作mysql数据的几个函数：
                    $n1 = mysql_num_rows(结果集);	//获得该结果集的数据行数；
                    $n2 = mysql_num_fields(结果集);	//获得该结果集的数据列数；
                    $name = mysql_field_name(结果集, $i );	//获得结果集的第i个字段的名字！i从0开始算起
            8,视图（view）定义语句
                
                语法形式：
                    create  view  视图名 【（字段名1，字段名2，字段名3，....）】   as   select语句；
