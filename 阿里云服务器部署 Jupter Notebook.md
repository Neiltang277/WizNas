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
```
$ yum install openssl-devel bzip2-devel expat-devel gdbm-devel readline-devel sqlite-devel
```

2、下载python3
```
$ wget https://www.python.org/ftp/python/3.6.0/Python-3.6.0.tgz
```

3、解压并进入目录
```
$ tar -xzvf Python-3.6.0.tgz -C  /tmp
$ cd  /tmp/Python-3.6.0/
```

4、修改python3的安装目录
```
$ ./configure --prefix=/usr/local
```

5、安装成功后的Python3文件目录
```
$ python3.6程序的执行文件：/usr/local/bin/python3.6
$ python3.6应用程序目录：/usr/local/lib/python3.6
$ pip3的执行文件：/usr/local/bin/pip3.6
$ pyenv3的执行文件：/usr/local/bin/pyenv-3.6
```

6、更改/usr，个人建议，最好保留原有的python2，用python3命令的方式使用python3，这样可以保证其他linux应用调用python时不会出现问题
```
$ ln -s /usr/local/bin/python3.6 /usr/bin/python3
$ ln -s /usr/local/bin/pip3.6 /usr/bin/pip3
```

**ps: 如果有需要更改/usr/bin/python系统自带的python链接：**

```
$ cd/usr/bin
$ python python.backup
$ ln -s /usr/local/bin/python3.6 /usr/bin/python
$ ln -s /usr/local/bin/python3.6 /usr/bin/python3
```
如遇到部分命令打开失效，则需要更改相关的配置文件：
```
#!/usr/bin/python 改为 #!/usr/bin/python2
```

---

## 2. 安装iPython和Jupyter

1. pip方式安装
```
$ pip3  install ipython
$ pip3 install jupyter
```
2. 生成Jupyter配置文件
```
jupyter notebook --generate-config
```

3. 生成密码: 打开ipython,创建密文密码
```
In [1]: from notebook.auth import passwd
In [2]: passwd()
	Enter password: 
	Verify password: 
Out[2]: 'sha1:*******'
```
将生成的sha1密码保存下。

4. 修改默认配置文件
```
# vi ~/.jupyter/jupyter_notebook_config.py
```

做如下修改
```
c.NotebookApp.ip='*' # 就是设置所有ip皆可访问
c.NotebookApp.password = u'sha1:ce...刚才复制的那个密文'
c.NotebookApp.open_browser = False # 禁止自动打开浏览器
c.NotebookApp.port =80 #随便指定一个端口，为方便起用了http默认端口80
```

5. 启动jupyter notebook
```
jupyter notebook
```
6. 关闭jupyter notebook
terminal界面使用ctrl+c关闭;
如果ssh连接断开重新连接时会，重新连接后使用：
```
ps -ef|grep jupyter
```
查询jupyter线程，使用kill关闭线程。


7. 使用nohup命令后台运行
```
$ nohup jupyter notebook &
```
查看任务列表
```
$ jobs
```

使用 fg %n关闭


---

## 未测试流程:
**需要输入密码访问，传输基于ssh**
1.生成秘钥
```
$ openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout key_cert.pem -out key_cert.pem
```
2. 有了key_cert.pem文件后可以先测试下正确性，使用如下方式启动Jupyter：
```
$ ipython notebook --certfile=key_cert.pem
```
如果浏览器打开的地址为https开头，那就成功了。

3. 重新更改ipython_notebook_config.py文件：
```
c.NotebookApp.certfile = u'/absolute/path/to/your/certificate/key_cert.pem'
```
4. 启动服务

