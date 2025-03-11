# 关于Jupyter导出pdf时不显示中文的问题

jupyter 导出 pdf 或 html 文件时，会出现不显示中文的问题

如果是anaconda3 自带的jupyter，则需要将 [pandoc](https://pandoc.org/installing.html) 安装到本地，如果是虚拟环境，激活环境后，可以用 pip 安装：

```python
pip install pandoc
```

要想显示中文，有几种方法，这里推荐一种简单而且一劳永逸的方法：

在虚拟环境中，windows路径为`/Users/xxx/anaconda3/share/jupyter/nbconvert/templates/latex/`,Linux路径为`/home/xxx/.conda/envs/python39/share/jupyter/nbconvert/templates/latex`的位置里找到 `index.tex.j2` 文件，然后打开，将其中的 `" article" 改成 "ctexart"`。最后，重启 jupyter，此时即可导出中文 pdf 或 html 文件。

<h1>参考</h1>

- Releseason. (2024, July 15). *Jupyter导出pdf或html时，显示中文并隐藏输入（有效版）*. CSDN. https://blog.csdn.net/qq_42535748/article/details/140437286

![image-20250311062443314](.Jupyter_nbconvert_file/image-20250311062443314.png)