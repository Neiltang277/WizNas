# Syllabus
> Description：
> 系统环境：CentOS 7

1. 安装 Python3，（系统自带Python2，如无要求，可使用系统自带版本）
2. 安装iPython和Jupyter
3. 配置Jupyter
4. 启动服务器
5. 关闭服务器

---

## 1. 安装 Python3

1、安装python3.6的相关依赖
> \# yum install openssl-devel bzip2-devel expat-devel gdbm-devel readline-devel sqlite-devel

2、下载python3
> \# wget https://www.python.org/ftp/python/3.6.0/Python-3.6.0.tgz

3、解压并进入目录
> \# tar -xzvf Python-3.6.0.tgz -C  /tmp
> \# cd  /tmp/Python-3.6.0/

4、修改python3的安装目录
> \# ./configure --prefix=/usr/local

5、安装成功后的Python3文件目录
> \# python3.6程序的执行文件：/usr/local/bin/python3.6
> \# python3.6应用程序目录：/usr/local/lib/python3.6
> \# pip3的执行文件：/usr/local/bin/pip3.6
> \# pyenv3的执行文件：/usr/local/bin/pyenv-3.6

6、更改/usr，个人建议，最好保留原有的python2，用python3命令的方式使用python3，这样可以保证其他linux应用调用python时不会出现问题
> \# ln -s /usr/local/bin/python3.6 /usr/bin/python3
> \# ln -s /usr/local/bin/pip3.6 /usr/bin/pip3

ps: 如果有需要更改/usr/bin/python系统自带的python链接：
> \# cd/usr/bin
> \# // 备份原有的python
> \# mv  python python.backup
> \# ln -s /usr/local/bin/python3.6 /usr/bin/python
> \# ln -s /usr/local/bin/python3.6 /usr/bin/python3


7、

