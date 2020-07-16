# QUBIC-实验1
## 所使用的数据集为 BicatYeast
## 操作步骤
```
> #加载程序包
> library("QUBIC")
> data("BicatYeast")
> matrix1 <- BicatYeast[1:7, 1:4]
> matrix1
```
- 输入数据确认了矩阵行与列的大小，7行4列  
![](https://github.com/ShiChenbin/biclusters/blob/master/QUBIC(BicatYeast)-img/%E8%BE%93%E5%85%A5%E6%95%B0%E6%8D%AE.png?raw=true)
- 将matrix1矩阵离散化并且存入变量matrix2中，可以发现矩阵内容都变为-1,0,1  
![](https://raw.githubusercontent.com/ShiChenbin/biclusters/master/QUBIC(BicatYeast)-img/%E7%A6%BB%E6%95%A3matrix1%E5%88%B0matrix2%E4%B8%AD.png)
- 将BicatYeast数据集导入x当中  
![](https://github.com/ShiChenbin/biclusters/blob/master/QUBIC(BicatYeast)-img/%E8%B5%8BBicatYeast%E5%88%B0x%E5%90%8C%E6%97%B6%E5%BC%80%E5%A7%8B%E8%AE%A1%E6%97%B6.png?raw=true)
- 加载色  
![](https://github.com/ShiChenbin/biclusters/blob/master/QUBIC(BicatYeast)-img/%E7%83%AD%E5%9B%BE%E5%88%B6%E4%BD%9C.png?raw=true)
- 输出热图（We can draw heatmap for single bicluster.）  
![](https://github.com/ShiChenbin/biclusters/blob/master/QUBIC(BicatYeast)-img/%E7%83%AD%E5%9B%BE%E5%91%88%E7%8E%B0.png?raw=true)  
We can draw heatmap for overlapped biclusters.  
```
par(mar = c(5, 5, 5, 5), cex.lab = 1.1, cex.axis = 0.5, cex.main = 1.1)
paleta <- colorRampPalette(rev(brewer.pal(11, "RdYlBu")))(11)
quheatmap(x, res, number = c(2, 3), showlabel = TRUE, col = paleta)
```
![](https://github.com/ShiChenbin/biclusters/blob/master/QUBIC(BicatYeast)-img/%E9%87%8D%E5%8F%A0%E7%9A%84%E9%85%B5%E6%AF%8D%E8%8F%8C%E5%8F%8C%E8%81%9A%E7%B1%BB%E7%83%AD%E5%9B%BE.png?raw=true)  
上图:在酿酒酵母数据中鉴定出的第二和第三双聚类的热图。Bicluster #2 (左上)由53个基因和5种条件组成，而Bicluster #3(右下)由37个基因组成
基因和7种条件。
```
net <- qunetwork(x, res, number = 2, group = 2, method = "spearman")
if (requireNamespace("qgraph", quietly = TRUE))
qgraph::qgraph(net[[1]], groups = net[[2]], layout = "spring", minimum = 0.6,
color = cbind(rainbow(length(net[[2]]) - 1), "gray"), edge.label = FALSE)
```
绘制关系图
![](https://github.com/ShiChenbin/biclusters/blob/master/QUBIC(BicatYeast)-img/%E8%81%9A%E7%B1%BB%E5%85%B3%E7%B3%BB%E5%9B%BE1%EF%BC%88%E6%94%B9%E9%83%A8%E5%88%86%E4%BB%A3%E7%A0%81%E5%AD%98%E5%9C%A8%E9%97%AE%E9%A2%98%EF%BC%89.png?raw=true)  