# GitLab升级与备份指南

本指南针对`CentOS7`编写，其他版本应该大同小异。

## 备份

一条命令完成备份

```bash
gitlab-rake gitlab:backup:create
```

使用以上命令会在`/var/opt/gitlab/backups`目录下创建一个名称类似为`1539937151_2018_10_19_11.3.6-ee_gitlab_backup.tar`的压缩包，这个压缩包就是`Gitlab`整个的完整备份，其中开头的`1539937151_2018_10_19_11.3.6`是备份创建的时间戳和日期。

## 升级

前往清华镜像站下载最新版本RPM包，下载地址：[https://mirrors.tuna.tsinghua.edu.cn/gitlab-ee/yum/el7/](https://mirrors.tuna.tsinghua.edu.cn/gitlab-ee/yum/el7/)

注意，请升级到当前版本的最新版本之后再升级到下一个版本的最新版本，大版本之前应该依次升级，比如当前版本是`10.5.6`，最新版本为`12.0.0`，那么升级流程应该是先升级到`10.8.7`，然后升级到11的最新版本`11.x.x`，最后再升级到`12.0.0`。

1、关闭部分gitlab服务

```bash
gitlab-ctl stop unicorn
gitlab-ctl stop sidekiq
gitlab-ctl stop nginx
```

2、升级

```bash
rpm -Uvh gitlab-ee-11.3.6-ee.0.el7.x86_64.rpm
```

3、重新配置gitlab

```bash
gitlab-ctl reconfigure
```

4、重启gitlab

```bash
gitlab-ctl restart
```

## 参考链接

[git学习------> Gitlab如何进行备份恢复与迁移？](https://blog.csdn.net/ouyang_peng/article/details/77070977)

[gitlab 升级](https://www.cnblogs.com/straycats/p/7707359.html)