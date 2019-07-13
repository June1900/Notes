#  Windows下安装不同版本MySQL

##  官网下载MySQL不同版本压缩包

* 下载MySQL压缩包，并解压（下载地址：<https://www.mysql.com/downloads/>）

* 在解压后的MySQL根目录创建my.ini文件

* 在新创建的文件中添加以下内容

  ~~~shell
  [mysqld]
  # 设置3307端口,安装两个mysql服务端口号不可以相同
  port=3307
  # 基本文件，数据文件，端口号，server_id都要是唯一的
  server_id = 1
  # 设置mysql的安装目录
  basedir="D:\\Dev\\mysql-8.0" 
  # 设置mysql数据库的数据的存放目录
  datadir="D:\\Dev\\mysql-8.0\\mysqldata"
  sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES 
  #修改了8.0版本密码的加密机制，如果不修改，将出现无法登录的情况
  default-authentication-plugin=mysql_native_password
  # 允许最大连接数
  max_connections=500
  # 允许连接失败的次数。这是为了防止有人从该主机试图攻击数据库系统
  max_connect_errors=10
  # 服务端使用的字符集默认为utf8mb4
  character-set-server=utf8mb4
  # 创建新表时将使用的默认存储引擎
  default-storage-engine=INNODB
  [mysql]
  # 设置mysql客户端默认字符集
  default-character-set=utf8mb4
  [client]
  # 设置mysql客户端连接服务端时默认使用的端口
  port=3307
  default-character-set=utf8mb4
  ~~~

##  安装MySQL服务

* 以管理员身份运行cmd，进入MySQL安装目录的bin目录，执行以下命令

  ~~~shell
  #第一种命令
  mysqld --defaults-file=D:\Dev\mysql-8.0\my.ini --initialize --console
  #第二种命令，没有--console，会在初始化完毕后，会在解压目录下生成一个data文件夹，这个文件夹下有一个.err结尾的文件，打开后会有随机生成的密码
  mysqld --defaults-file=D:\Dev\mysql-8.0\my.ini --initialize
  ~~~

* 执行命令完成后，会生成以下内容

  ~~~
  2019-07-13T09:33:03.505439Z 0 [Warning] [MY-010915] [Server] 'NO_ZERO_DATE', 'NO_ZERO_IN_DATE' and 'ERROR_FOR_DIVISION_BY_ZERO' sql modes should be used with strict mode. They will be merged with strict mode in a future release.
  2019-07-13T09:33:03.505557Z 0 [System] [MY-013169] [Server] D:\Dev\mysql-8.0\bin\mysqld.exe (mysqld 8.0.16) initializing of server in progress as process 18584
  2019-07-13T09:33:30.551414Z 5 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: :S:2gagbn*cl
  2019-07-13T09:33:40.524893Z 0 [System] [MY-013170] [Server] D:\Dev\mysql-8.0\bin\mysqld.exe (mysqld 8.0.16) initializing of server has completed
  ~~~

* 安装服务

  ~~~
  mysqld install MySQL8
  或者指定默认配置文件安装服务
  mysqld install MySQL8  --defaults-file="D:\Dev\mysql-8.0\my.ini"
  ~~~

* 修改启动的mysqld文件

  ~~~
  打开windows的注册表（regedit），在\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services下找到对应的服务，修改ImagePath
  ~~~

* 修改完成后，启动MySQL服务

  ~~~
  net start MySQL8
  ~~~

##  登录MySQL修改密码

* 登录MySQL

  ~~~shell
  mysql -uroot -p -P3307
  #输入刚才保存的密码
  ~~~

* 修改MySQL密码

  ~~~mysql
  ALTER USER 'root'@'localhost'IDENTIFIED BY '**';
  ~~~

* 修改完成后就可以操作MySQL

  ~~~mysql
  # 查看数据库
  show databases;
  ~~~

##  注意

* 在遇到一直启动情况，所有操作都无法杀死进程，可以通过`taskkill /pi** /f`强制结束进程

* 删除服务名

  ~~~
  (1)采用windows自带的服务管理工具
  sc delete MySQL57
  (2)mysqld移除
  mysqld --remove MySQL57 
  ~~~

  