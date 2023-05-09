# ubuntu 上安装mysql并配置远程登陆

## 一、安装

> 1. 更新
>
>    ```shell
>    $ sudo apt-get update
>    $ sudo apt-get upgrade
>    ```
>
> 2. 安装
>
>    ```shell
>    $ sudo apt install mysql-server
>    $ sudo apt install mysql-client
>    ```
>
> 3. 确定是否安装完毕
>
>    ```shell
>    $ mysqladmin --version
>    ```
>
>    ![](https://github.com/hulk-ben/notebook/blob/master/image/%E6%88%AA%E5%9B%BE%202023-05-09%2016-48-39.png?raw=true)
>
> 4. 初始密码一般为空，如果是deb安装包会在/var/log/mysqld.log里
>
> 5. 启动服务
>
>    ```shell
>    $ sudo systemctl start mysqld
>    $ sudo systemctl status mysqld
>    ```
>
> 6. 登陆
>
>    ```shell
>    $ mysql -uroot -p
>    ```
>
>    ![](https://github.com/hulk-ben/notebook/blob/master/image/%E6%88%AA%E5%9B%BE%202023-05-09%2017-03-38.png?raw=true)

## 二、配置

> 1. 更改密码
>
> ```sql
> mysql> alter user 'root'@'localhost' identified by '12345';
> ```
>
> ![](https://github.com/hulk-ben/notebook/blob/master/image/%E6%88%AA%E5%9B%BE%202023-05-09%2017-08-09.png?raw=true)
>
> 2. 使用mysql库，将root的host改为想监听的地址或所有（%）,并刷新
>
> ```sql
> mysql> use mysql;
> mysql> select host,user from user;
> mysql> update user set host = '%' where user = 'root';
> mysql> flush privileges;
> ```
>
> ![](https://github.com/hulk-ben/notebook/blob/master/image/%E6%88%AA%E5%9B%BE%202023-05-09%2017-25-13.png?raw=true)
>
> 3. 将配置文件/etc/mysql/mysql.conf.d/mysqld.conf更改为监听所有地址,并重启服务
>
> ![](https://github.com/hulk-ben/notebook/blob/master/image/%E6%88%AA%E5%9B%BE%202023-05-09%2017-52-00.png?raw=true)
>
> 4. 连接
>
> ```shell
> $ mysql -uroot -h 192.168.56.5 -p
> ```

## 其他问题

> 在用root账户登陆时会提示错误![](https://github.com/hulk-ben/notebook/blob/master/image/%E6%88%AA%E5%9B%BE%202023-05-09%2018-10-56.png?raw=true)
>
> 可以进入数据库更改验证模块
>
> 
>
> ``` mysql
> mysql > update user set plugin = 'mysql_native_password' where user='root';
> mysql > alter user 'root'@'%' identified by '12345';
> mysql > flush privileges;
> ```
>
> 

> 

