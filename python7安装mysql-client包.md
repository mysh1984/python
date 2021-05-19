参考：

https://blog.csdn.net/weixin_40947719/article/details/86323073



## 一、环境说明 

| python环境 | 3.7       |
| ---------- | --------- |
| OS环境     | Win10 x64 |





## 二、包说明

使用Django、flask等来操作MySQL，实际上底层还是通过Python来操作的。因此我们想要用Django来操作MySQL，首先还是需要安装一个驱动程序。在Python3中，驱动程序有多种选择。比如有pymysql以及mysqlclient等

常用驱动：

MySQL-python：也就是MySQLdb。是对C语言操作MySQL数据库的一个简单封装。遵循了Python DB API v2。但是只支持Python2，目前还不支持Python3。

mysqlclient：是MySQL-python的另外一个分支。支持Python3并且修复了一些bug



## 三、安装

3.1、下载

从以下地址下载

```htm
https://pypi.org/project/mysqlclient/#files
```

下载文件

mysqlclient-2.0.3-cp37-cp37m-win_amd64.whl



3.2、安装

执行命令

```po
C:\Users\aaa>pip install mysqlclient-2.0.3-cp37-cp37m-win_amd64.whl
Processing c:\users\ubt\mysqlclient-2.0.3-cp37-cp37m-win_amd64.whl
Installing collected packages: mysqlclient
Successfully installed mysqlclient-2.0.3
```

检测下是否成功安装mysqlclient,输入python,然后输入：import MySQLdb

若未报错则安装成功！

```pow
C:\Users\aaa>python
Python 3.7.4 (tags/v3.7.4:e09359112e, Jul  8 2019, 20:34:20) [MSC v.1916 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> import MySQLdb
>>>
```





## 四、使用

```pow
>>> from MySQLdb import Connect
>>> db = MySQLdb.connect(host='10.10.1.12',port=3306,user='root',password='abcd1234',db='mqtt')
>>> c = conn.cursor()
>>> c.execute("""use mqtt""")
0
>>> c.execute("""select * from mqtt_client""")
1
>>> r = c.fetchone()
>>> print(r)
(1, '111', 'testName', 1, 'aaa', 'bbb', 'dd', '1.0.0', '2.0.0', datetime.datetime(2020, 3, 4, 13, 57, 22), datetime.datetime(2020, 3, 4, 13, 57, 25))
>>>
```

