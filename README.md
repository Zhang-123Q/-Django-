# -Django-
# 基于Django的多终端点餐系统 v1.0

## 1.摘要
本项目为个人学习过程中完成的练习项目，主要学习Django的相关知识，适合新手学习，除前段html的相关文件外，其余文件均为个人实操完成，但项目设计和源代码并非原创，均来自哔哩哔哩up主【拉勾教育】[说明：并非广告，尊重原创]。

**欢迎关注个人哔哩哔哩账号：我家公子Q**
**欢迎关注个人微信公众号：运筹帷幄Q**

项目以Django为开发框架进行系统的设计和开发，数据库采用的是MySQL，设计并开发了网页端、移动端和管理后台三个终端。其中网页端主要是模拟现实下的大堂点餐场景，配合触摸屏，即可完成大堂点餐的操作（请读者自行脑补xx奶茶店门店的点餐场景）；移动端是模拟现实下的手机移动端点餐，比如通过手机扫码点餐；后台管理主要是对菜品、店铺、管理员等信息进行管理，即后台信息管理系统。

本文档就技术需求、各模块内容及如何快速体验进行简单介绍。
## 2.技术需求
- 数据库：MySQL
- 网站开发架构：Django
- 编程语言：python（前端为javaScript）
- 系统开发平台：Vscode

因为本项目主要针对Django进行训练，因此其他内容的技能要求并不高。其中，MySQL数据库仅需要练习者掌握MySQL的安装，数据库管理员的设置，数据库的创建等基础操作，在此作者建议直接使用数据库可视化工具Navicat进行操作；当然练习者需要对python基础编程知识有所掌握；前端知识可以稍微了解一下（简单熟悉相关的标签）；系统开发平台Vscode、Pycharm等都可以，作者已测试。
## 3.数据库相关
数据库设计首先进行概念设计，概念模型的常用的表示方法是用实体-联系方法（Entity Relationship Approach, E-R方法）。

本项目涉及的实体主要包括：员工、店铺、菜品类别、菜品、顾客（会员）、订单、订单详情、支付信息。

完整的E-R图如下所示：
![h4A2i.png](https://s1.328888.xyz/2022/05/03/h4A2i.png)
关于数据库的创建，一方面，练习者可以使用MySQL直接进行数据库和相关表格的创建，然后进行表格内部数据的调用；另一方面，可以先创建数据库后，然后连接好数据库，使用数据迁移的方式进行各个数据表的创建。

本项目有些表格已经有数据，便于进一步的功能测试，文末也给出了相关的SQL文件。

## 4.功能模块
本项目主要分为web端（大堂点餐端）、移动端和后台管理端。各部分的主要功能如下列框架所示。
![AxUCT.png](https://s1.328888.xyz/2022/05/02/AxUCT.png)

现将各终端功能进行简要说明。
### 4.1 myadmin（后台管理端）
本部分首先需要登录操作：
![AMOw1.png](https://s1.328888.xyz/2022/05/02/AMOw1.png)
登录后进入浏览页面，需要注意的是这里涉及Django的中间件配置，即只有成功登录后才可以进行后续的各项操作。

![Ax9EZ.png](https://s1.328888.xyz/2022/05/02/Ax9EZ.png)
需要注意的是，此处的前端模板来自AdminLTE开源模板。

在后台管理系统中，已经完成关于员工的登录、退出操作，员工信息管理操作，店铺信息管理操作，菜品信息管理（其中包含菜品种类信息管理和菜品信息管理两个子模块），订单管理，会员（顾客）信息管理模块。

信息管理是指相关模块信息的增、删、改、查操作，反映到代码框架上则基本表现为六项视图方法：

- 信息浏览方法（index）
- 加载信息添加表单（add）
- 执行信息添加操作（insert）
- 执行信息删除（delete）
- 加载信息编辑表单（edit）
- 执行信息编辑（update）
  
该部分在项目架构中的myobject >> myadmin文件夹

需要说明的是，本项目的路径形式为：[http://主机名:端口/应用名/视图名/函数名]
### 4.2 web端（大堂点餐端）
首先，在大堂点餐端也需要完成点餐系统的登录。
![hgojZ.png](https://s1.328888.xyz/2022/05/03/hgojZ.png)

首先需要完成店铺选择，然后进行账号密码的登录，这里可以使用【账号：zhangs 密码：123】进行测试。

需要特别注意的是，此处添加了验证码的生成与验证操作，可以详细看项目代码中关于验证码的相关方法。

登入系统后首页面，如下图所示。
![hgPzg.png](https://s1.328888.xyz/2022/05/03/hgPzg.png)

左侧为购物车模块，右侧为菜品显示模块，显示模块主要设涉及分页操作及记录的增删改查等操作。

可以通过点击购买，将相对应的菜品添加至购物车，然后选择相关的支付方式进行订单提交。

然后上方横向菜单栏，可以选择当前订单、历史订单、无效订单等进行浏览。
![h99Im.png](https://s1.328888.xyz/2022/05/03/h99Im.png)

最后，可以通过右上角的“退出”按钮，实现账号的退出。

### 4.3 mobile端（移动端）
移动端与大堂点餐端的视图类似，基本设计思路也是快速登录-实现菜品浏览-菜品选购等操作。不同的主要存在两个方面：
（1）移动端的页面尺寸不同，主要面向手机、平板等终端；
（2）添加了个人主页

首先是快速登录界面。移动端可以在网页上通过右键“检查”，然后点击终端切换按钮，进行测试。
![hf4tQ.png](https://s1.328888.xyz/2022/05/03/hf4tQ.png)

可以在数据库中选择相关的手机号码进行登录【比如：12345678909】，但是这里并没有连接发送短信的API接口，仅放置了一分钟倒计时按钮。测试验证为1234。

进入首页后，与大堂点餐类似，首页为菜品浏览界面，但是界面浏览方式与大堂点餐有所区别，左侧以侧边栏选项卡的形式展示菜品类别，然后右侧显示当前店铺下每一个菜品类别下的菜品。

![hf7ag.png](https://s1.328888.xyz/2022/05/03/hf7ag.png "首页")

当前需要特别说明的是，如果是一开始登录，则默认出现的店铺选择界面，首先完成店铺的选择，然后才会进一步跳转到该界面。

当然，在当前页面也可以进行店铺的切换操作。在当前页面，点选菜品的购物车小按钮，则会将该菜品添加至购物车，然后可以进一步通过点击“去结算”按钮跳转至结算界面。

![hfY4t.png](https://s1.328888.xyz/2022/05/03/hfY4t.png)

添加购物车，点击“去结算”：

![hfcNO.png](https://s1.328888.xyz/2022/05/03/hfcNO.png)

提交订单则完成订单的提交操作。

在“首页”中，点击“我的”，即可进入个人主页。

![hf30P.png](https://s1.328888.xyz/2022/05/03/hf30P.png)

此处可以实现账号内的订单浏览和账号退出操作。“我的订单”显示如下：

![hfZSJ.png](https://s1.328888.xyz/2022/05/03/hfZSJ.png)


## 5.待完善部分
本项目目前是1.0版本的订餐系统，基本的功能模块已经实现，但是存在许多细节的完善，需要进一步完善的部分主要有以下几个：

- 后台管理系统中权限管理模块并未完成相关设计
- 后台管理系统中首页的相关数据可视化的视图并没有展示出来
- 后台管理系统中对于菜品的描述可结合富文本编辑器进行操作
- web端和移动端的支付模块并没有对应添加支付宝或微信支付的接口
- 移动端快速登录中验证码实际接受与反馈的实现
- 移动端个人主页中我的资料、修改密码等操作并没有实现，也并未在数据库设计中进行相关内容的设计和二者的连接
  
## 6.快速开始
这里，假设你是一个并未接触过Django系统开发设计的小白白，但是你想体验一把这牛皮（LaJi）的系统。你需要按照以下步骤启动服务。

### 6.1 下载代码文件到本地
下载链接为：

### 6.2 运行SQL文件，搭建项目数据库
相关sql文件已经放置在项目文件夹中。
- 进入MySQL数据库中，创建一个数据库名为：osdb
- 将上节《项目的数据库设计》中准备好的osdb.sql脚本导入到osdb数据库中
### 6.3 使用VSCode打开项目文件
配置数据库，在myobject >> setting.py文件中进行数据库连接。

```python
...
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'osdb',
        'USER': 'root',  # 使用你自己的数据库账户
        'PASSWORD': 'ZZQ123',  # 使用你自己的数据库密码
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
...
```
### 6.4 启动服务
- 定位到项目根目录（manage.py文件所在的文件夹下），启动终端：
可以选择在VSCode中直接启动，快捷键为"ctrl+`"，
也可以通过在文件地址栏输入cmd回车启动，

- 然后输入"python manage.py runserver 0.0.0.0:8080"
点击回车即可启动服务。
**注意上方启动命令中，“0.0.0.0:8080”内容可以省略，默认启动8000端口，要是想以别的端口打开，可以写8080或者其他。**

打开浏览器，在地址栏输入相应地址即可打开。
http.localhost:8000 默认进入web端
http.localhost:8000/myadmin 进入后台
http.localhost:8000/mobile  进入移动端

*******
## 写在最后
再次声明，本项目内的系统并非作者原创，仅供学习使用。
欢迎关注微信公众号：运筹帷幄Q
![hhBk7.jpg](https://s1.328888.xyz/2022/05/03/hhBk7.jpg)
也欢迎关注哔哩哔哩Up主：我家公子Q


