---
title: 该怎样使用textappearance属性？
date: 2016-08-01 20:32:55
categories: 
  - android
tags: 
  - android
  - textappearance
---

在阅读http://blog.danlew.net/2014/11/19/styles-on-android/ 时，文中提到尽可能使用textAppearance
> **Rule #4: Use text appearance when possible.**

那么问题来了，该如何使用呢？当textAppearance属性值对应的样式和style属性值的样式都有定义时，会如何呢？
来来来，带着问题上路，让实践告诉我们！
设定一个TextView的属性如下
```
android:textColor="#ffffff"
android:textAppearance="@style/TitleAppearance"
```
其中的TitleAppearance如下
```
<style name="TitleAppearance" parent="TextAppearance.AppCompat">
    <item name="android:textColor">@color/colorAccent</item>
</style>
```
最后应用的还是`android:textColor="#ffffff"`这一声明。
另外，文章中提到的另一点也是值得注意的
>Notice how I've set a parent - text appearances won't merge, so you need to make sure to define all attributes. You can use any appropriate TextAppearance
 as the parent.

实践中通过继承`TextAppearance.AppCompat.Large`，结果也确实是没有将`TextAppearance.AppCompat.Large`中的设置继承下来，文本的大小并没有受影响。
```
<style name="TitleAppearance" parent="TextAppearance.AppCompat.Large">
</style>
```

综合之前的实践，那么应该怎样来使用这个属性呢？
两者都定义冲突，反而是style中的样式获胜，也就是说两者同时声明时，如果style中也包含针对text相关属性设置时，textAppearance属性的定义就是多余的。由此得出，两者的关注点不同，textAppearance作为一种更具体（针对text）的样式，应该作为style的补充，即专门针对text，而普通style中则不应该有针对text的相关设定为好。
