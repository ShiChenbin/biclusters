# QUBIC
## 介绍
一种双聚类算法,就其在生物数据解释中的效率和有效性而言，QUIBIC被公认为是最佳的双聚类方法之一。
## 软件包
该软件包提供了QUBIC算法的R实现，具有显着提高的效率和完善的功能。
## 说明书
http://bioconductor.org/packages/QUBIC
## 前提
首要第一步，请检查您的R语言的版本，打开电脑中的 R x64  
![](https://github.com/ShiChenbin/biclusters/blob/master/QUBIC-img/R%E8%AF%AD%E8%A8%80%E8%BD%AF%E4%BB%B6.png?raw=true)
  
输入version查看当前版本，3.6.3以下建议更新，不是最新版本都建议更新
![](https://github.com/ShiChenbin/biclusters/blob/master/QUBIC-img/R-%E6%9F%A5%E7%9C%8B%E7%89%88%E6%9C%AC.png?raw=true)

输入进行更新
```
updateR() 
```

最后返回true才说明更新成功

### 1
要安装QUBIC的开发版本，您至少需要从CRAN安装以下软件包
```
install.packages("biclust")
```
安装聚类包，这是安装成功的情况
![](https://github.com/ShiChenbin/biclusters/blob/master/QUBIC-img/%E5%AE%89%E8%A3%85biclust.png?raw=true)  

```
install.packages("Rcpp")
```
安装RCPP包，这也是生物信息学R语言中十分常见的（如果出现错误提示，那么说明你的R语言版本是较早的，而RCPP是不兼容的）
![](https://github.com/ShiChenbin/biclusters/blob/master/QUBIC-img/%E5%AE%89%E8%A3%85RCPP.png?raw=true)

```
install.packages("RcppArmadillo")
```

```
source("http://bioconductor.org/biocLite.R") # install BiocInstaller
```
(在之前进行FABIA算法的运行我的BIOC包已经是安装完毕了，也就不必再进行重复安装)
### 提示
如果出现无法安装并且提示是rstdio版本问题或者是Bioc包版本较旧的问题，所以需要更新版本  
参考 https://blog.csdn.net/u014801157/article/details/62884401
### 2
对于Windows用户，还应该安装Rtools（https://cran.r-project.org/bin/windows/Rtools/）。

#### 配置环境
1）在RStudio里面运行以下脚本：
配置环境变量  
```
writeLines('PATH="${RTOOLS40_HOME}\\usr\\bin;${PATH}"', con = "~/.Renviron")
```
2）重新启动RStudio，然后运行以下代码：
```
Sys.which("make")
```
会得到结果："C:\\rtools40\\usr\\bin\\make.exe"（也就是make.exe的路径）

3）尝试安装一个包
```
install.packages("jsonlite", type = "source")

```
如果安装成功，则说明 Rtools 可以使用了！
### 安装QUBIC包
```
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install("QUBIC")
```
![](https://github.com/ShiChenbin/biclusters/blob/master/QUBIC-img/QUBIC%E5%8C%85%E5%AE%89%E8%A3%85.png?raw=true)
#### 查看说明书
```
browseVignettes("QUBIC")
```
会直接跳转网页，给出了大体的操作方式，有需要可以自己去浏览。

### 3
然后，

```
install.packages("devtools")
devtools::install_github("zy26/QUBIC")
```

要绘制热图并可视化网络，还应该安装以下软件包：
```
install.packages("qgraph")
install.packages("RcolorBrewer")
```

小插图
您可以在https://bioconductor.org/packages/release/bioc/vignettes/QUBIC/inst/doc/qubic_vignette.pdf上找到QUBIC的教程。

## 开始试验

```
library("QUBIC")
```
加载QUBIC包，成功加载的结果如下：
![](https://github.com/ShiChenbin/biclusters/blob/master/QUBIC-img/%E5%8A%A0%E8%BD%BDQUBIC%E5%8C%85.png?raw=true)  
### 第一个程序编写和运行结果

![](https://github.com/ShiChenbin/biclusters/blob/master/QUBIC-img/%E7%AC%AC%E4%B8%80%E4%B8%AA%E8%BF%90%E8%A1%8C%E7%BB%93%E6%9E%9C.png?raw=true)
### 第二个程序编写和运行结果
![](https://github.com/ShiChenbin/biclusters/blob/master/QUBIC-img/%E7%AC%AC%E4%BA%8C%E4%B8%AA%E7%A8%8B%E5%BA%8F%E8%BF%90%E8%A1%8C.png?raw=true)
### 显示聚类热图
```
# show heatmap 我直接放在这里了，因为需要输入的十六进制代码比较多，所以直接复制也比较方便
hmcols <- colorRampPalette(rev(c("#D73027","#FC8D59","#FEE090","#FFFFBF","#E0F3F8","#91BFDB", "#4575B4")))(100)
```
![](https://github.com/ShiChenbin/biclusters/blob/master/QUBIC-img/%E7%83%AD%E5%9B%BE%E6%98%BE%E7%A4%BA.png?raw=true)  

### 前面这些运行下来，各变量数据情况如下
![](https://github.com/ShiChenbin/biclusters/blob/master/QUBIC-img/%E5%8F%98%E9%87%8F%E6%83%85%E5%86%B51.png?raw=true)
