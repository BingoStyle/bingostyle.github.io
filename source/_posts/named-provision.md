---
title: 命名provision的使用
date: 2016-07-27 20:44:31
categories: 
  - development
tags: 
  - vagrant
  - provisioning
---

除了用provisioning来安装软件外，有些时候也需要有针对的执行一些脚本，比如部署或者配置变更需重启某些软件，这时，命名Provision就能派上用场了。

## 命名Provision的声明和使用
[官方文档](https://www.vagrantup.com/docs/provisioning/basic_usage.html)对命名provisioning的描述，如下：
> Provisioners can also be named (since 1.7.0). These names are used cosmetically for output as well as overriding provisioner settings (covered further below). An example of naming provisioners is shown below
```
Vagrant.configure("2") do |config|
  # ... other configuration
  config.vm.provision "bootstrap", type: "shell" do |s|
    s.inline = "echo hello"
  end
end
```
> Naming provisioners is simple. The first argument toconfig.vm.provision becomes the name, and then a type option is used to specify the provisioner type, such as type: "shell" above.

版本1.7开始支持这种方式的，我所用的版本1.8.4是支持的。声明方式也就是在参数最前新增一个名称参数，比如示例中`onfig.vm.provision "bootstrap", type: "shell" do |s|`的"bootstrap"。

知道如何声明了，那该如何执行命名provisioning呢？继续阅读[官方文档](https://www.vagrantup.com/docs/provisioning/basic_usage.html)
>The arguments to --provision-with  can be the provisioner type (such as "shell") or the provisioner name (such as "bootstrap" from above).

结果就是通过`vagrant provision --provision-with bootstrap`运行

### 参考
[provisioning基本用法](https://www.vagrantup.com/docs/provisioning/basic_usage.html)