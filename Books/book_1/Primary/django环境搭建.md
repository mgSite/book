# centos7 部署django环境
## 部署mysql
- 离线安装mysql
## 部署redis
- 离线安装redis
## 部署python依赖环境
- 离线安装python依赖
## 部署python
- 离线安装python


# 在线安装
- 参考：https://www.cnblogs.com/ianduin/p/7679239.html
```

//换源
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
yum makecache

yum update
yum upgrade
wget http://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm
yum localinstall mysql57-community-release-el7-8.noarch.rpm
yum repolist enabled | grep "mysql.*-community.*"
yum install mysql-community-server

systemctl start mysqld


systemctl enable mysqld
systemctl daemon-reload

//查看默认root密码
grep 'temporary password' /var/log/mysqld.log

//修改mysql默认密码

shell> mysql -u root -p
mysql> show variables like '%password%';
mysql> set global validate_password_policy=0;
mysql> set global validate_password_length=1;
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'mm123'; 
mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'mm123' WITH GRANT OPTION;
mysql> FLUSH  PRIVILEGES;

//python依赖
yum install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel libffi-devel gcc make
//python 升级

wget -P /usr/local  http://www.python.org/ftp/python/3.8.5/Python-3.8.5.tgz
cd /usr/local
tar -xzvf Python-3.8.5.tgz -C /usr/local

mkdir /usr/local/python3
cd /usr/local/Python3.8.5
./configure --prefix=/usr/local/python3
make && make install

mv /usr/bin/python /usr/bin/python_old2

ln -s /usr/local/python3/bin/python3 /usr/bin/python

```
