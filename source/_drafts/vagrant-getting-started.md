---
title: vagrant-getting-started
tags: vagrant
---

## 为什么要使用vagrant

## 快速入门

```shell
% mkdir vagrant_project
% cd vagrant_project 
% vagrant init centos/6
```

`vagrant init`后会在当前文件夹下产生一个名为Vagrantfile的文件

编辑其内容：

```
config.vm.box = "~/Downloads/centos-6.5-x86_64-minimal.box"
config.vm.box_check_update = false
```

这时，可以选择使用`vagrant up`，或使用下载工具先将box文件下载到本地的，下载的好处是即能节约时间，也便于共享。如果不想使用最新版本，也可以禁用更新检查。

接着，可以

```
% vagrant up 
% vagrant ssh #若成功，则意味着连上了虚拟环境了
```

使用同步功能:

默认情况下，client os中的/vagrant目录与host os初始化目录同步，也就是说虚拟系统中的/vagrant与宿主系统初始化vagrant项目时目录同步。比如：

* 在宿主系统中

  ```vagrant_project touch abc
  vagrant_project touch abc
  ```

  则虚拟系统中/vagrant目录下则会多出abc文件。

* 在虚拟系统中

  ```
  [vagrant@localhost /]$ touch /vagrant/foo
  ```

  则宿主系统中vagrant_project下则会多出foo文件。



