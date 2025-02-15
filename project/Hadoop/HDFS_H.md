# HDFS 的基础操作

HDFS是分布式文件系统，但是在HDFS的API下，就像在操作本地文件一样

## HDFS基本操作

查看文件

文件的添加

文件的修改

文件的删除

删除文件

## 列出目录内容

```
hdfs dfs -ls <path>
```

**示例**

```
hdfs dfs -ls /
```

![image-20250214164916322](https://db.xinghai.ink/Typora/17395229615700352.png)

```
hdfs dfs -ls /abc
```

![image-20250214165005002](https://db.xinghai.ink/Typora/17395230069582777.png)

## 创建目录

```
hdfs dfs -mkdir <path>
```

**示例**

```
hdfs dfs -mkdir /file
```

![image-20250214165519262](https://db.xinghai.ink/Typora/17395233210132463.png)

```
hdfs dfs -mkdir -p /file/abc/abc/aaa/e
```

![image-20250214165633593](https://db.xinghai.ink/Typora/17395233963216605.png)

## 创建空文件

```
hdfs dfs -touch /aaa.txt
```

![image-20250214165948865](https://db.xinghai.ink/Typora/17395235910314822.png)

## 上传文件或文件夹

```
hdfs dfs -push <filepath> <hdfspath>
```

**示例**

```
hdfs dfs -put ./test.txt /file/
```

![image-20250214170250357](https://db.xinghai.ink/Typora/17395237732143211.png)

```
hdfs dfs -put ./test.txt /file/ae.txt
```

![image-20250214170405980](https://db.xinghai.ink/Typora/1739523847925945.png)

```
hdfs dfs -put ./bb /
```

![image-20250214172034251](https://db.xinghai.ink/Typora/173952483628187.png)

## 查看文件内容

```
hdfs dfs -cat <path>
```

**示例**

```
hdfs dfs -cat /bb/test8.txt
```

![image-20250214174937090](https://db.xinghai.ink/Typora/17395265838825986.png)

```
hdfs dfs -cat /bb/*
```

![image-20250214175023486](https://db.xinghai.ink/Typora/17395266251598003.png)

## 删除文件

```
hdfs dfs -rm <path>
```

![image-20250214175119981](https://db.xinghai.ink/Typora/17395266821078186.png)

```
hdfs dfs -ls -r /file
```

![image-20250214175207018](https://db.xinghai.ink/Typora/17395267288522708.png)

## 移动文件/重命名文件

```
hdfs dfs -mv /abc /aaa
```

![image-20250214175257386](https://db.xinghai.ink/Typora/1739526779411698.png)

```
hdfs dfs -mv /bb/test2.txt /
```

![image-20250214175354231](https://db.xinghai.ink/Typora/17395268361061325.png)

## 下载文件

```
hdfs dfs -get <path>
```

![image-20250214175658891](.HDFS_H_file/17396309218551352.png)



<h1>参考</h1>

- 恒悦sunsite. (2021, December 23). *Hadoop之hadoop Fs命令*. CSDN. https://blog.csdn.net/carefree2005/article/details/122081314
- 风从安城起. (2024, March 7). *HDFS常见命令练习（二）*. CSDN. https://blog.csdn.net/fly66666666/article/details/136524205


<div style="color:red;float:right;"><sub>2025年02月14日</sub></div>