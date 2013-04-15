# 基于SAML的IDP设计

	本项目是为毕业设计使用的，没有其他用途

## 模型说明

通常情况下，一个公司内部的服务需要单独管理用户，而SSO的出现使得公司可以统一管理用户，一个用户在一个公司内只需要一个帐号。

此时当用户需要登录的时候，会跳转到一个IDP服务器上进行登录，登录成功后,IDP向原服务器返回登录数据。

但是此时每个公司仍旧需要一个独立的用户管理系统。

而此项目将不同公司间的SSO服务器进行**统一管理**

提供给每个公司一个**虚拟**的IDP服务器。

公司内部用户在访问资源的时候先跳转到虚拟的IDP服务器进行登录，然后再返回到资源服务器。

优点：公司**不需要**自行管理用户服务器，降低数据丢失和内部人员盗窃数据的风险，降低管理成本。

缺点：将用户托管在云端，这本身就是一种风险,一旦云端服务器被攻破，所有公司的数据都会被获取到。而且当断网的时候无法登录。

## LDAP

LDAP是轻量目录访问协议，使用树状的层次结构来存储数据，可以将其类比成UNIX文件树。

## LDAP优点

1. 读取性能优越，适合大量读的场合
2. 应用程序不需要存储数据库帐号，安全
3. 通过不同的分支可以进行逻辑隔离
4. 非常方便的管理用户和组织

尤其是其安全功能，是本项目的重点。
传统的DBMS都需要应用程序存储一个数据库帐号，一旦应用程序被攻破，数据库也随之被攻破。而LDAP并不存在数据库帐号这么个东西，LDAP中用户既是数据，又是帐号，每个用户可以使用自己的帐号去连接LDAP数据库，同样，管理员帐号也作为LDAP中的一个普通节点存在。
用户身份验证可以使用多种方法，最基本的如密码验证，高级一点的还支持证书验证和OTP验证。

## 功能说明

    
### 超级管理员提供的功能

1. 超级管理员登录
	
	
2. 配置各个租户的信息

  * 新建租户 **租户只能由超级管理员新建，暂不提供自助注册**
  * 修改租户 
  * 查看租户列表 
  * 查看网站统计数据

	服务器通过租户名生成一个唯一的IDP URL，同时生成LDAP数据库中一个分支，各租户间的信息相互隔离。

3. 

### 给租户管理员提供的功能

1. 

### 给用户提供的功能

1.  
2.  

### 运行流程
