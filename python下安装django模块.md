##  一、环境描述

| OS     | Win10 X64 |
| ------ | --------- |
| Python | 3.7       |



## 二、安装django

2.1、安装

```bash
pip install Django==3.2.3
```



2.2、验证

```po
C:\Users\ubt>python
Python 3.7.4 (tags/v3.7.4:e09359112e, Jul  8 2019, 20:34:20) [MSC v.1916 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> import django
>>> django.get_version()
'3.2.3'
>>>
```





## 三、使用django

3.1、创建工程

```bash
C:\Users\ubt>django-admin startproject testproject
C:\Users\ubt>cd testproject
```

3.2、创建application

```bash
C:\Users\ubt\testproject>python manage.py startapp test1
```

3.3、初始化django自带的表

```bash
C:\Users\ubt\testproject>python manage.py migrate

Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying admin.0003_logentry_add_action_flag_choices... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying auth.0010_alter_group_name_max_length... OK
  Applying auth.0011_update_proxy_permissions... OK
  Applying auth.0012_alter_user_first_name_max_length... OK
  Applying sessions.0001_initial... OK
```



3.4、启动

```po
C:\Users\ubt\testproject>python manage.py runserver 127.0.0.1:8000
```



3.5、访问

通过以下地址访问

```bash
http://127.0.0.1:8000/
```



通过以下地址访问后台管理

```bash
http://127.0.0.1:8000/admin
```



3.6、修改后台管理用户和密码

```power
C:\Users\ubt\testproject>python manage.py createsuperuser
Username (leave blank to use 'atoon'): admin
Email address: 111@qq.com
Password:
Password (again):
The password is too similar to the username.
This password is too short. It must contain at least 8 characters.
This password is too common.
Bypass password validation and create user anyway? [y/N]: y
Superuser created successfully.
```

使用新建的用户登录后台管理界面