# 双聚类算法-FABIA  
## 前提
1.Rstdio 的下载和安装  
R version >= 4.0.0.
2.安装R语言的相关包到Rstdio中 
 - 在Rstdio左下方Console，这个是Rstdio的控制台，能够输入R语言运行的结果，同时也能对Rstdio进行一些操作

3.常用的R包：可参考 https://support.rstudio.com/hc/en-us/articles/201057987-Quick-list-of-useful-R-packages  

4.按应用领域分类的R包，可参考 https://cran.r-project.org/web/views/  

5.安装过程中会出现试开url字样，请内心等待加载条加载完毕

### 包的安装：
```
install.packages("包的名字")  
```
### 包的信息查询
```cpp
help(package = "babynames")
```

### 包的加载：
用library(包的名字)
  
### 从环境中移除包：
detach("package:包的名字", unload=TRUE)  

### 卸载包：
remove.packages("包的名字")  

## install BiocManager

### 介绍
这是R的生物信息学包

## BiocManager 安装
1.打开Rstdio
2.将如下内容输入到控制台中
```cpp
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install()
```
输出结果  
```cpp
package ‘BiocManager’ successfully unpacked and MD5 sums checked

The downloaded binary packages are in
	C:\Users\DELL\AppData\Local\Temp\RtmpKIIS49\downloaded_packages
```
说明R生物信息学包已经安装成功

## fabia安装

### 介绍
生物信息学fabia双聚类算法包？  

###安装代码
```cpp  
BiocManager::install("fabia")
```
返回结果
```
package ‘BiocGenerics’ successfully unpacked and MD5 sums checked
package ‘Biobase’ successfully unpacked and MD5 sums checked
package ‘BiocVersion’ successfully unpacked and MD5 sums checked
package ‘fabia’ successfully unpacked and MD5 sums checked

The downloaded binary packages are in
```

## 查询fabia基本功能
```
help(package="fabia")
```
然后出现这个
![](https://github.com/ShiChenbin/biclusters/blob/master/R-img/FABIA-help.png?raw=true)

## fabia

 - 加载fabia包 library(fabia) 选中该语句 ctrl+enter 进行执行操作
 - FABIA EXAMPLE 1 样例1 代码
 ```r
library(fabia)
n=200
l=100
p=4
dat <- makeFabiaDataBlocks(n = n,l= l,p = p,f1 = 5,f2 = 5,of1 = 5,of2 = 10,sd_noise = 3.0,sd_z_noise = 0.2,mean_z = 2.0, sd_z = 1.0,sd_l_noise = 0.2, mean_l = 3.0,sd_l = 1.0)
X <- dat[[1]]
ZC <- dat[[3]]
LC <- dat[[4]]
gclab <- rep.int(0, l)
gllab <- rep.int(0, n)
clab <- as.character(1:l)
llab <- as.character(1:n)
for (i in 1:p){
  for (j in ZC[i]){
   clab[j] <- paste(as.character(i),"_",clab[j],sep="")
   }
  for (j in LC[i]){
  llab[j] <- paste(as.character(i),"_",llab[j],sep="")
   }
  gclab[unlist(ZC[i])] <- gclab[unlist(ZC[i])] + p^i
  gllab[unlist(LC[i])] <- gllab[unlist(LC[i])] + p^i
}
groups <- gclab
write.csv(X, file="datafile.csv")
write.table(groups, file = "groups.txt")
write.table(clab, file = "clabels.txt")
write.table(llab, file = "rlabels.txt")
```
代码运行成功后的结果
![](https://github.com/ShiChenbin/biclusters/blob/master/R-img/example-1.png?raw=true)

 - 读取“datafile.csv” 文件数据和标签
 ```cpp
    X <- read.table("datafile.csv", header = TRUE, sep = ",")
    X <- as.matrix(X[, -1])
    groups <- read.table(file = "groups.txt")
    clab <- read.table(file = "clabels.txt")
    llab <- read.table(file = "rlabels.txt")
    colnames(X) <- 1:ncol(X)
    rownames(X) <- 1:nrow(X)
```
没有明显报错就说明运行成功了不要惊慌 ovo
- 基于前面的数据建立模型
    - 基因数据可以通过 View(X) 进行查看
    ![](https://github.com/ShiChenbin/biclusters/blob/master/R-img/view-X.png?raw=true)
 ```cpp
res <- fabia(X, 4, 0.1, 400, 1, 1)
```
![](https://github.com/ShiChenbin/biclusters/blob/master/R-img/example-1-res.png?raw=true)

- 显示聚类信息
```cpp
res@avini
```

显示结果
[1] | 60.63664  54.46367  48.10243  45.32622  208.52732

 
5. 汇总:  
First, it gives the number or rows and columns of the original matrix and then the number of
clusters. Then for the row cluster the information content is given. Then for each column its
information content is given. Then for each cluster a column summary is given by a boxplot.
Finally, for each cluster a row summary is given by a boxplot.  
译文：   
首先，它给出原始矩阵的行数和列数，然后是簇数。然后给出行集群的信息内容。然后给出每一列的信息内容。然后，对于每个集群，最后通过箱线图给出列摘要。对于每个集群，箱线图给出行摘要

代码
```cpp
summary(res)
```
![](https://github.com/ShiChenbin/biclusters/blob/master/R-img/example-1-summary.png?raw=true)  
6.显示 ：  

可以在右侧查看结果图片一共是4张图片
![](https://github.com/ShiChenbin/biclusters/blob/master/R-img/example-1-figure1.png?raw=true)  
![](https://github.com/ShiChenbin/biclusters/blob/master/R-img/example-1-figure2.png?raw=true)  
![](https://github.com/ShiChenbin/biclusters/blob/master/R-img/example-1-figure3.png?raw=true)  
![](https://github.com/ShiChenbin/biclusters/blob/master/R-img/example-1-figure4.png?raw=true)  
