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





