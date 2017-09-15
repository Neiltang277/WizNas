**准备工作，安装Virtualenv**
```
pip3 install virtualenv
```

**第一步，创建目录：**
```
mkdir myproject
```

**第二步，创建一个独立的Python运行环境，命名为venv：**
```
virtualenv --no-site-packages venv
```

**新建的Python环境被放到当前目录下的venv目录。有了venv这个Python环境，可以用source进入该环境：**
```
source venv/bin/activate
```

**退出当前的venv环境，使用deactivate命令：**
```
deactivate 
```
