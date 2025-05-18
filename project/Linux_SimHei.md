<div class="container">

# 关于Linux中matplotlib没有SimHei中文字体的问题</div>

在linux中使用matplotlib时，为了避免中文乱码，通常会将字体修改成`SimHei`中文字体，但是Linux中并没有这个字体，所以需要安装

## 下载`SimHei`

<h3>链接下载</h3>

通过链接`https://us-logger1.oss-cn-beijing.aliyuncs.com/SimHei.ttf`，下载SimHei字体到本地

```
wget https://us-logger1.oss-cn-beijing.aliyuncs.com/SimHei.ttf
```

![image-20250119110811225](https://db.xinghai.ink/Typora/17372560952587707.png)

<h3>通过windows复制</h3>

windows默认带有`SimHei`字体，以我的`windows11`为例在`C:\Windows\WinSxS\amd64_microsoft-windows-font-truetype-simhei_31bf3856ad364e35_10.0.26100.1_none_f11b5ebedca17dd9`路径下就可以找到`SimHei`字体

![image-20250119112834517](https://db.xinghai.ink/Typora/17372573199577482.png)

然后将它上传到linux即可

## 安装`SimHei`字体

在linux中，将字体文件放在`/usr/share/fonts`即安装成功

```
cp SimHei.ttf /usr/share/fonts/
```

**刷新系统缓存**

```
fc-cache -fv
```

这样在系统中就安装成功了

但是在这个时候`matplotlib`还是找不到`SimHei`字体,因为matplotlib会在自己的字体库中查找字体

解决办法是，找到`python`的`matplotlib`库文件夹，以我的conda为例，`matplotlib`字体库路径在`/home/xinghai/app/conda/envs/public/lib/python3.9/site-packages/matplotlib/mpl-data/fonts/ttf`文件夹中，将`SimHei.ttf`文件复制到这里

```
cp SimHei.ttf /home/xinghai/app/conda/envs/public/lib/python3.9/site-packages/matplotlib/mpl-data/fonts/ttf
```

然后清除matplotlib缓存，缓存路径在`~/.cache`中，删除即可

```
rm -rf ~/.cache
```

这样就可以了

## 总结

`matplotlib`使用不了`SimHei`字体有可能是应为`matplotlib`字体库中没有`simhei`字体文件，解决方法是将`simhei`字体文件放在`simhei`字体库中并删除`matplotlib`缓存

<h2>参考</h2>

- Jlb1024. (2019, December 19). SimHei字体（永久有效）. Retrieved January 19, 2025, from https://blog.csdn.net/jlb1024/article/details/98037525
- Embeddebugger. (2021, November 30). Linux下matplotlib无法显示中文字体. https://blog.csdn.net/weixin_47965042/article/details/121632927

<div style="color:red;float:right;"><sub>2025年01月19日</sub></div>