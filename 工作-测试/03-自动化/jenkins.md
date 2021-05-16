## 前言

持续部署

持续集成

持续交付

作用：

1. 降低风险
2. 减少重复过程
3. 任何时间、任何地点
4. 增强项目的可见性
5. 建立团队对项目的信心

#### jenkins 和 hudson

原本是一个项目，后面分离了



## 安装

1. 安装jenkins前确保您的电脑已经配置好JDK

   JDK下载地址:https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html

2. 下载好jenkins安装包

   jenkins下载地:https://jenkins.io/

#### 一、Jdk安装

新版本直接下载傻瓜式安装就可以

测试是否安装成功

![image-20210317201006765](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210317201006765.png)

若是安装不成功配置环境变量

计算机右键 》属性 》高级系统设置 》 高级 》 环境变量

配置 Path 和 JAVA_HOME

![img](https://img2018.cnblogs.com/blog/1421063/201809/1421063-20180929095726883-1409282461.png)

![img](https://img2018.cnblogs.com/blog/1421063/201809/1421063-20180929100830114-940600833.png)

#### 二、安装 Jenkins

1. 下载好后直接双击安装，安装好后自动打开浏览器，打开页面，默认为8080端口（可以自己修改）

> 注：要是打不开，可能是 java jdk 有问题，重新下载安装试试

2. 打开界面后，去路径下找到密码输入

![image-20210317201436287](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210317201436287.png)

3. 第一个默认安装，第二个手动选择

   ![img](https://img2018.cnblogs.com/blog/1421063/201809/1421063-20180929111824912-1810722533.png)

4. 安装完成后，创建用户

   ![image-20210317201655588](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210317201655588.png)

5. 创建用户后默认选择，打开主界面

   ![image-20210317201815125](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210317201815125.png)

6. 之后就可以使用了

## 使用

#### 修改语言

Manage Jenkins 》Manage plugins

![image-20210317203246947](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210317203246947.png)

当中文不完全的时候，安装两个包都，第一个需要进行配置，第二个不需要

![image-20210317203355538](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210317203355538.png)



Manage Jenkins 》Manage System 

先修改 zh_US，重启，在修改为 zh_CN, 刷新页面即可

![image-20210317203512042](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210317203512042.png)

重启应用即可

#### 基本操作

**启动**

```
java -jar jenkins.war 
```

**重启**：http://localhost:30001/restart  

**重载**：http://localhost:30001/reload

**停止**：http://localhost:30001/exit



#### 基本配置

全局安全配置（学习）

- 允许用户注册
- 任何用户做任何事

全局工具配置

- maven配置路径
- JDK 配置
- maven 配置

插件安装

- Deploy to container





