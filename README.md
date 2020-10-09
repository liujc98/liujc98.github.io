# 个人主页
#### 更新这个主页也算是为了记录一些日常关键的信息
## 常用的访问链接 
[从零开始的生物信息学](https://zhuanlan.zhihu.com/c_1060579529482948608)

[The Django Book](http://djangobook.py3k.cn/2.0/)

[算法导论-MIT](https://www.bilibili.com/video/BV1Tb411M7FA?from=search&seid=9248342711021682564)

[Learn Vim Progressively](http://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/)

[Raindy 的网络硬盘](http://raindy.ys168.com/)

[生物信息学教案](https://app.yinxiang.com/fx/31ac2fb0-ca34-4df3-b794-14ac88237a73)

[Learn Python the hard way.3rd](http://shouce.jb51.net/python-way/learn-python-the-hard-way-appendix-a-Introduction.html)

[鸟哥的linux私房菜 基础学习篇](http://cn.linux.vbird.org/linux_basic/linux_basic.php)
## 平时上课用到的代码，今后也会更新一些作业中用到的新代码并进行一些注解
下面备注的是更新的时间
### 用于从docker中copy文件到桌面（反之亦然）
2020/9/25
    
    docker cp bioinfo_tsinghua:/home/test/mapping Desktop/bioinfo_tsinghua_share
    
### 用于去掉列中的“”和；的方法
2020/9/28
    
    cat 1.gtf | awk ' $3 == "CDS" && $1 == "XI" {split($10,x,";");name = x[1]; gsub("\"","",name);print $5,name}' | sort -n | tail
    
### 解压缩
2020/9/30
    
    unzip bash_homework.zip
    
### 输出文件名称的代码
2020/10/5
    
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
2020/10/6 
    
    应该注意 `\t` 和 ` 反引号 `的使用
    
## Jupyter notebook中只有Python 3
2020/10/9
    
从官网下载的anaconda3 中自带Jupyter notebook，但是里面只有Python3
想要将Python2也安装进去，因为电脑中有Pymol，首先要注意安装的位置，不要安装在Pymol的同级文件夹中
    
    # 打开Anaconda Prompt，留意地址目录，输入
    jupyter kernelspec list
    
得到结果

    Available kernels:
        python3    C:\123\share\jupyter\kernels\python3
        python2    C:\ProgramData\jupyter\kernels\python2
        
其中一个C:\123是我anaconda安装的路径，没有安装python2则不会显示第二个路径
继续在Anaconda Prompt中操作

    conda create --name python27 python=2.7 #安装python2环境
    conda install ipykernel #安装python2内核
    python -m ipykernel install #配置内核
    # 再打开jupyter notebook即可
    # 如果中途出现如下情况
    Fatal Python error: init_sys_streams: can't initialize sys standard streams
    LookupError: unknown encoding: 65001
    # 则
    set PYTHONIOENCODING=utf-8
    
参考网站

1[anaconda 中启动jupyter notebook找不到python2 kernerl](https://blog.csdn.net/u013187057/article/details/83689020)

2[Jupyter Notebook介绍、安装及使用教程](https://www.jianshu.com/p/91365f343585)

3[Jupyter notebook 里面没有python3怎么办?](https://blog.csdn.net/qq_41500222/article/details/81129603)

4[查看Jupyter-Python核](https://blog.csdn.net/woai8339/article/details/82767356)

5[Fatal Python error](https://blog.csdn.net/qq_42303913/article/details/103645226)
    
