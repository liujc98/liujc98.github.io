# Web note
更新这个主页也算是为了记录一些日常关键的信息

2020/10/19

说是个人主页，其实好像更像是笔记一样的东西，因此更名为Web Note

## 常用的访问链接 
[从零开始的生物信息学](https://zhuanlan.zhihu.com/c_1060579529482948608)

[The Django Book](http://djangobook.py3k.cn/2.0/)

[算法导论-MIT](https://www.bilibili.com/video/BV1Tb411M7FA?from=search&seid=9248342711021682564)

[Learn Vim Progressively](http://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/)

[Raindy 的网络硬盘](http://raindy.ys168.com/)

[生物信息学教案](https://app.yinxiang.com/fx/31ac2fb0-ca34-4df3-b794-14ac88237a73)

[Learn Python the hard way.3rd](http://shouce.jb51.net/python-way/learn-python-the-hard-way-appendix-a-Introduction.html)

[鸟哥的linux私房菜 基础学习篇](http://cn.linux.vbird.org/linux_basic/linux_basic.php)

[廖雪峰的Python教程](https://www.liaoxuefeng.com/wiki/1016959663602400)

# 平时上课用到的代码，今后也会更新一些作业中用到的新代码并进行一些注解
下面备注的是发现问题的时间，更新时间可以在GitHub中找到
## Linux
下面是在linux中运行的代码，包括但不限于docker，shell等子应用
从2020/9/21 开始学习linux
下面是上课和自学中遇到的一些需要Mark的问题，留个备注以便之后查阅
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

### 平时写代码时应该注意的问题
2020/10/6 
    
    应该注意 `\t` 和 ` 反引号 `的使用
        
### 运行shell时使用sh命令报错
2020/10/11

    # Shell的调用文件命令分很多种，如
    sh read.sh
    bash read.sh
    ./read.sh
    # 上述的三种表述方法其实并不完全一致，经常性的会在第一种sh命令时报错
    # 只需改用其余的两种方式就应该可以修正，说明linux在不同的版本之间个别的语句不相互兼容
    # 更进一步的说，sh所调用的只是bash的一个子集
    
## R
2020/10/12

开始看R，先从R_in_A开始看，记录一下书里的关键代码，以及对代码的一些理解

### 建立组合图像
2020/10/14

    attach(mtcars)
    layout(matrix(c(1,1,2,3), 2, 2, byrow = TRUE))
    hist(wt)
    hist(mpg)
    hist(disp)
    detach(mtcars)
    
这是初看之下无法理解的代码思路，我认为简单地理解方式应该是
建立了一个2X2矩阵 

1 1

2 3

这个矩阵将要放着我们的图像，因此图像1放在了数字1的位置图像2/3同理
于是就变成了图像1占据了窗口的上半部分，图像2/3分别在左下和右下
    
### transform和with/within 
2020/10/15

    # 当我想要在原始的数据框中添加新的列向量时
    # 创建数据框mydata，x1和x2是mydata的两个列向量
    mydata <- data.frame(x1 = c(2, 2, 6, 4), x2 = c(3, 4, 2, 8))

    # 利用transform函数对数据框mydata增加两个变量（列向量）sumx和meanx，并把结果存储在数据框mydata中
    mydata <- transform(mydata, sumx = x1 + x2, meanx = (x1 + x2)/2)

    # 利用within函数，expr表达式执行一条语句占一行，执行多条语句需要换行
    mydata <- within(mydata, {sumx = x1 + x2
                         meanx = (x1 + x2)/2})

    # 或者多条语句在同一行，则中间应当用分号;隔开
    mydata <- within(mydata, {sumx = x1 + x2; meanx = (x1 + x2)/2})
    
参考网站

[transform函数与with/within函数](https://zhuanlan.zhihu.com/p/25847796)

### R语言的可视化——在直方图上添加密度曲线
2020/10/16

在做题的过程中遇到了这样的问题，参考了网上的很多代码找到了这个比较合适的，首先`set.seed(1234)`是为了保证每次产生的随机数一致
在curve中按照如下的形式给出参数，可以看到curve的参数较为独特，可以直接根据`dnorm`绘制曲线，更为关键的是dnorm中的参数`x`
仅是首次出现就可以执行代码的功能，目前还不够理解其中的原因，留待之后探究

    set.seed(1234)
    score <- rnorm(n = 1000, m = 80, sd = 20)
    hist(score, freq=FALSE, xlab="Score", main="Distribution of score", 
     col="lightgreen", xlim=c(0,150), ylim=c(0, 0.02))
    curve(dnorm(x, mean=mean(score), sd=sd(score)), 
      add=TRUE, col="darkblue", lwd=2)

综合来说用于实现这个功能的代码数量很多，对于密度曲线的理解也因人而异，如果是只是要画本函数的对应密度函数，那么应该使用如下的代码
借助`prob=T`和`density()`可以实现画图，需要注意的是这样画出来肯定不是一个正态分布曲线，更应该是一个弯曲的密度函数曲线
另外`lines()`这个函数属于是“底层作图”，所以不需要`add = T`这样的语句

    set.seed(123)
    h<-rnorm(1000)
    hist(h,prob=T,col="light blue")
    lines(density(h), col="red", lwd=3)  
    
 画正态分布曲线的方法这里也再给出一种，借助`lines()`函数可以绘制正态曲线，但是需要在画图之前先建立一些间隔点，并依据如下的参数进行构建
    
    cache<-seq(3.5, 6.5, length.out=100)
    lines(cache, dnorm(cache, 5, 0.316), col="blue")

## Python
2020/10/17

开始正式自学Python，先从廖雪峰的Python课程开始
记录一下书里的关键代码，以及对代码的一些理解

2020/10/19

我觉得廖雪峰的Python教程写的很好，也比较符合我当前的需求，最近也会抽时间更新一些学习过程中应该注意的事项，
并且，目前的计划和打算是看完Python后可以掌握如何去写一些基本的网页并利用**爬虫**，这个目标定得应该是比较高的，但是目前还是希望可以好好完成

### Jupyter notebook中只有Python 3
2020/10/3
    
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

1.[anaconda 中启动jupyter notebook找不到python2 kernerl](https://blog.csdn.net/u013187057/article/details/83689020)

2.[Jupyter Notebook介绍、安装及使用教程](https://www.jianshu.com/p/91365f343585)

3.[Jupyter notebook 里面没有python3怎么办?](https://blog.csdn.net/qq_41500222/article/details/81129603)

4.[查看Jupyter-Python核](https://blog.csdn.net/woai8339/article/details/82767356)

5.[Fatal Python error](https://blog.csdn.net/qq_42303913/article/details/103645226)

2020/10/16
后记：这是很早就开始做出的更改，最开始的目的是为了匹配《Learn Python the Hard Way 3rd》中的教程所做的，
但是很快随着平时的一些查阅资料发现，目前来说学习Python2并不是最好的选择，Python3才具备更为明显的时代特征和方向性，
因此Python2只是作为一个安装的教程出现的，如果可以的话也留待之后进一步的学习

### 关于Python学习的一些观点记录/建立新的Repo用来存放需要的图片
2020/10/19

看到了很多的Python方面的教程和方法，加上最近的自学，个人觉得廖雪峰的Python课程写的很好，
也是在知乎上看到了有关Python学习的一些方向性指导，这里附上一张图片，也供自己之后查看
建立了一个新的Repo，我觉得这是我目前看到的十分便捷的用来存放图片的方法，也可以很好地插入图片到MD里面去

![Ways to Python](https://github.com/liujc98/MyImages/raw/main/Ways%20to%20Python.jpg)

图源[各个阶段Python的学习方法](https://www.zhihu.com/question/44337172/answer/202958210)
    
