
# 个人主页
## 常用的访问链接
[从零开始的生物信息学](https://zhuanlan.zhihu.com/c_1060579529482948608)

[The Django Book](http://djangobook.py3k.cn/2.0/)

[算法导论-MIT](https://www.bilibili.com/video/BV1Tb411M7FA?from=search&seid=9248342711021682564)

[Learn Vim Progressively](http://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/)

[Raindy 的网络硬盘](http://raindy.ys168.com/)

[生物信息学教案](https://app.yinxiang.com/fx/31ac2fb0-ca34-4df3-b794-14ac88237a73)
## 平时上课用到的代码，今后也会更新一些作业中用到的新代码并进行一些注解
### 用于从docker中copy文件到桌面（反之亦然）
    
    docker cp bioinfo_tsinghua:/home/test/mapping Desktop/bioinfo_tsinghua_share
    
### 用于去掉列中的“”和；的方法
    
    cat 1.gtf | awk ' $3 == "CDS" && $1 == "XI" {split($10,x,";");name = x[1]; gsub("\"","",name);print $5,name}' | sort -n | tail
    
### 解压缩
    
    unzip bash_homework.zip
    
### 输出文件名称的代码
    
    echo $CUR_DIR
    for val in $CUR_DIR
    do
        # 若val是文件，则输出该文件名到filename.txt
        if [ -f $val ];then
                echo "FILE: $val" >> filename.txt
        # 若val是文件夹，则输出该文件夹名到dirname.txt
        elif [ -d $val ];then
                echo "DIR: $val" >> dirname.txt
        fi
    done
    exit 0

## 平时写代码时应该注意的问题
2020/10/6 应该注意 `\t` 和 ` 反引号 `的使用
