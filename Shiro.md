##shiro简介
###(1)什么是shiro
Apache shiro是一个强大易用的Java安全框架,提供了认证,授权.加密和会话管理等功能:

认证 - 用户身份识别,常被称为用户"登录",判断用户是否登录,如果未登录则进行拦截其请求;

授权 - 访问控制,当用户登录后,判断其身份是否有权限访问相应的资源,如果没有权限则拦截;

加密 - 保护或隐藏数据防止被偷窥;将MD5进行了二次封装,让其更易用.注意MD5不可逆运算.
###(2)Shiro主要有四个组件
* SecurityManager
	
	典型的Facade,Shiro通过他对外提供安全管理的各种服务.
* Authenticator
	
	对"Who are you ?"进行核实.通过设计用户名和密码.
	
	这个组件负责收集principals和credentials,并将它们提交给应用系统.如果提交的credentials跟应用系统中提供的credentials吻合,就能继续访问,否则需要重新提交principals和credentials,或者直接终止访问.
	
* Authorizer

	身份验证通过后,由这个组件对登录人员进行访问控制的筛查,比如"who can do what",或者"who can do which acitons".SHiro采用"基于Realm"的方法,即用户(又称Subject),用户组,角色和permission的聚合体.
	
* Session Manager
	
	这个组件保证了异构客户端的访问,配置简单.它是基于POJO/J2SE的,不跟任何的客户端或者协议绑定.
	
###(3)Shiro运行原理
![](图片路径)

1.**Application Code:**应用程序代码,就是我们自己的编码,如果在程序中需要进行权限控制,需要调用Subject的API.

2.**Subject:**主体,代表了当前用户.所有的Subject都绑定到SecrityManager,与Subject的所有交互都会委托给SecurityManager,可以将Subject当成一个门面,而真正的执行者是SecurityManager.

3.**SecurityManager:**安全管理器,所有与安全有关的操作都会与SecurityManager交互,并且它管理所有的Subject.

4.**Realm:**域Shiro是从Realm获取安全数据(用户,角色,权限).就是手偶SecurityManager.

要验证用户身份,那么它需要从Realm获取相应的用户进行比较以确定用户身份是否合法;也需要从Realm得到用户相应的角色/权限进行验证用户是否能进行操作,可以吧Realm看成DataSource,即安全数据源

###(4)Shiro为程序共提供了四种权限控制方式

url级别权限控制

方法注解权限控制

代码级别权限控制

页面标签权限控制

###(5)认证与Shiro安全框架

1. 传统登录方式

	![](图片链接)

2. Shiro安全框架实现登录

	![](图片链接)
	
###(6)授权的实现流程(粗颗粒和细颗粒权限)

1. 什么是粗颗粒和细颗粒权限?
2. 粗颗粒和细颗粒如何授权?

###(7)本系统权限模型
