```
    //获取输入
    echo "Input you name"
    read NAME
    echo "Hello,$NAME"
    //变量
    var1 = "value1"
    var2 = var1
    //
    for skill in Java C++
    do 
        echo 'i am good at ${skill} Script'
    done
    

# bash常用 判断

# 　　1）判断表达式

# 　　if test  (表达式为真)
# 　　if test !表达式为假
# 　　test 表达式1 –a 表达式2                  两个表达式都为真
# 　　test 表达式1 –o 表达式2                 两个表达式有一个为真

# 　　2）判断字符串

# 　　test –n 字符串                                   字符串的长度非零
# 　　test –z 字符串                                    字符串的长度为零
# 　　test 字符串1＝字符串2                    字符串相等
# 　　test 字符串1！＝字符串2               字符串不等

# 　　3）判断整数

# 　　test 整数1 –eq 整数2                        整数相等
# 　　test 整数1 –ge 整数2                        整数1大于等于整数2
# 　　test 整数1 –gt 整数2                         整数1大于整数2
# 　　test 整数1 –le 整数2                         整数1小于等于整数2
# 　　test 整数1 –lt 整数2                          整数1小于整数2
# 　　test 整数1 –ne 整数2                        整数1不等于整数2

# 　　4）判断文件

# 　　test  File1 –ef  File2　　　　　　　　两个文件具有同样的设备号和i结点号
# 　　test  File1 –nt  File2　　　　　　　　文件1比文件2 新
# 　　test  File1 –ot  File2　　　　　　　　文件1比文件2 旧
# 　　test –b File　　　　　　　　文件存在并且是块设备文件
# 　　test –c File　　　　　　　　文件存在并且是字符设备文件
# 　　test –d File　　　　　　　　文件存在并且是目录
# 　　test –e File　　　　　　　　文件存在
# 　　test –f File 　　　　　　　　文件存在并且是正规文件
# 　　test –g File　　　　　　　　文件存在并且是设置了组ID
# 　　test –G File　　　　　　　　文件存在并且属于有效组ID
# 　　test –h File　　　　　　　　文件存在并且是一个符号链接（同-L）
# 　　test –k File　　　　　　　　文件存在并且设置了sticky位
# 　　test –b File　　　　　　　　文件存在并且是块设备文件
# 　　test –L File　　　　　　　　文件存在并且是一个符号链接（同-h）
# 　　test –o File　　　　　　　　文件存在并且属于有效用户ID
# 　　test –p File　　　　　　　　文件存在并且是一个命名管道
# 　　test –r File　　　　　　　　文件存在并且可读
# 　　test –s File　　　　　　　　文件存在并且是一个套接字
# 　　test –t FD　　　　　　　　文件描述符是在一个终端打开的
# 　　test –u File　　　　　　　　文件存在并且设置了它的set-user-id位
# 　　test –w File　　　　　　　　文件存在并且可写
# 　　test –x File　　　　　　　　文件存在并且可执行


#!/bin/sh
echo "Please input your name"
read PERSON
echo "Hello,${PERSON}"
# for循环
for loop in java php
    do 
        echo "i am good at $loop Script"
	done

echo $HOME
# while循环
COUNTER=0
while [ $COUNTER lt 5 ]
do
    COUNTER="expr $COUNTER+1"
    COUNTER = COUNTER+1
    echo $COUNTER
done
# 数组
my_array=(A B "C" D)
# 相等
num1=100
num2=100
if test $[num1] -eq $[num2]
then
    echo '两个数相等！'
else
    echo '两个数不相等！'
fi
# 函数
demoFun(){
    echo "这是我的第一个 shell 函数!"
}
echo "-----函数开始执行-----"
demoFun
echo "-----函数执行完毕-----"

# # 运算符	说明	举例
# -eq	检测两个数是否相等，相等返回 true。	[ $a -eq $b ] 返回 true。
# -ne	检测两个数是否相等，不相等返回 true。	[ $a -ne $b ] 返回 true。
# -gt	检测左边的数是否大于右边的，如果是，则返回 true。	[ $a -gt $b ] 返回 false。
# -lt	检测左边的数是否小于右边的，如果是，则返回 true。	[ $a -lt $b ] 返回 true。
# -ge	检测左边的数是否大等于右边的，如果是，则返回 true。	[ $a -ge $b ] 返回 false。
# -le	检测左边的数是否小于等于右边的，如果是，则返回 true	[ $a -le $b ] 返回 true。

# 1,简单shell模拟登录

echo -n "login:"
read name
echo -n "password:"
read password

if [ $name = "root" -a $password = "adc" ]; 
	then
	#statements
		echo "The Host and password is right"
	else
		echo "Host or password Error"

fi

# 2,比较两个数的大小

echo "Please enter two number"
read a
read b
if test $a -eq $b ; then
	#statements
	echo "a = b"
else 
	echo "a != b"
fi

# 3,查找/root/目录下是否存在该文件

echo "enter a file name"
read file
if test -e /root/$file; then
	echo "the file exists"
else	
	echo "the file is not exists"
fi


# 4.给函数传递参数

func() {
    num1=$1
    echo "--func--${num}"
}
func $@

# 5.检查端口号是否已启动

n=1
echo "检查3306 mysql 端口"

while true
do
        if test $n -gt 20
        then 
                echo "3306服务启动失败"
                break
        fi
                
        sleep 5
        n=$(($n+1))
        
        # port=`netstat -antp | grep "localhost:3306"`
        port = `netstat -nat | grep 3306`
        # port = `lsof -i tcp:3306`
        if [ ${#port} -gt 3 ]; then
                echo "3306服务已经启动"
                break;
        fi
done

