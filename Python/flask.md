### 使用 Flask-Script 支持命令行选项

服务器由 `manager.run()` 启动后就能解析命令行了。

默认支持 shell 和 runserver 两个命令：

- shell 命令用于在程序的上下文中启动 python shell 会话
- runserver 命令用于执行 `app.run()`

### 大型程序的结构

#### 需求文件

`pip freeze > requirements.txt` 生成需求文件

`pip install -r requirements.txt` 使用

### 部署

#### 配置选项

`export CONFIG_NAME='production'` 选择配置类

#### 应用容器

`pip install Gunicorn`

### 参考链接

- [Flask-Script](http://flask-script.readthedocs.io/en/latest/)
- [部署](https://spacewander.github.io/explore-flask-zh/13-deployment.html)