# 刘家琛的个人主页
## 常用的访问链接
[从零开始的生物信息学](https://zhuanlan.zhihu.com/c_1060579529482948608)

[The Django Book](http://djangobook.py3k.cn/2.0/)

[算法导论-MIT](https://www.bilibili.com/video/BV1Tb411M7FA?from=search&seid=9248342711021682564)

[Learn Vim Progressively](http://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/)

[Raindy 的网络硬盘](http://raindy.ys168.com/)

[百度](https://www.baidu.com)
## 平时上课用到的代码
### 用于从docker中copy文件到桌面（反之亦然）
    
    docker cp bioinfo_tsinghua:/home/test/mapping Desktop/bioinfo_tsinghua_share
    
### 用于去掉列中的“”和；的方法
    
    cat 1.gtf | awk ' $3 == "CDS" && $1 == "XI" {split($10,x,";");name = x[1]; gsub("\"","",name);print $5,name}' | sort -n | tail
    
###
