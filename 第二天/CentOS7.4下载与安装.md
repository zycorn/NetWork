# CentOS7.4下载与安装

标签（空格分隔）： Linux

---
# 一、CentOS7.4下载
> 官网下载页面地址：Index of/

## 1、进入CentOS下载官网，找到CentOS7.4版本
![image_1g3vgjhui1ughp03lk3o1s1mck9.png-123.4kB][1]
## 2、在CentOS7.4版本页面中，找到isos/
![image_1g3vgkh19128qc071clp1d91ke613.png-113kB][2]
## 3、进入页面后，可以看到x86_64
![image_1g3vglfm5mcoqn3nku1uab5f9.png-653.1kB][3]
## 4、在CentOS下载页面中，选择 CentOS-7-x86_64-DVD-1708.torrent进行下载
![image_1g3vgmn5g1e31s9m1c9nsft17v4m.png-183.8kB][4]
## 5、下载完成之后，由于“CentOS-7-x86_64-DVD-1708.torrent”只是一个BT种子文件，而且非常小，这就需要我们使用迅雷等工具来对源镜像进行下载了
> （1）打开迅雷，新建任务，把“CentOS-7-x86_64-DVD-1708.torrent”BT种子文件拖入到新建任务中，并点击立即下载
![image_1g3vgogif1qfe1o7lbgf8ilkcv13.png-34.4kB][5]

# 二、CentOS7.4安装
## 1、打开你的VMware Workstation Pro，并点击“创建新的虚拟机”
![image_1g3vgu61h1ph5qtn14fihgc12ae1g.png-90.6kB][6]
# 2、点选典型(推荐)(T)，并点击“下一步”
![image_1g3vh03c21dalg1k1rj84bu823.png-169kB][7]
# 3、点选稍后安装操作系统(S)，并点击“下一步”
![image_1g3vh12fs12501hkatqgmnv1t342g.png-153kB][8]
# 4、点选Linux(L)，因为我们之前下载的 CentOS-7-x86_64-DVD-1708.iso 是64位 7.4版本的，所以这里我们选择CentOS 7 64位，并点击“下一步”
![image_1g3vh36d41k081qa4kn1omrsn72t.png-154.8kB][9]
# 5、虚拟机名称可以更改也可以不更改看自己需求，修改虚拟机的安装路径，并点击“下一步”
![image_1g3vh8es71bs84ig317qa24m3a.png-140.8kB][10]
# 6、磁盘选择默认为20.0GB，点选将虚拟磁盘存储为单个文件(O)，并点击“下一步”
![image_1g3vhe53sio11asvj7k1u0e1hct3q.png-148.9kB][11]
# 7、点击“完成”，然后点击编辑虚拟机，将下载的镜像文件设置，然后点击确定
![image_1g3vhipep1elc17gmqpt1rdku6o4n.png-148.5kB][12]
# 8、开启虚拟机，鼠标移入到虚拟机中，并按下“↑”键，选择Install CentOS 7，最后按下“Enter 键”，最后再按下“Enter 键”
# 9、默认安装过程中的安装界面使用English (英语)可以去下面找到简体中文，点击“继续”
![image_1g3vhurmm8dafcn1ih42mn1afv9.png-168.5kB][13]
# 10、配置时区 (DATE & TIME)

>（1）选择DATE & TIME
![image_1g3vi0jl5op11m3c1q0qm93paj13.png-182.4kB][14]
> （2）时区设置为 Region：Asia    City：Shanghai日期和时间设置与自己的电脑时间同步，最后点击“确认”
![image_1g3vi5ki0b1p1dst9geo481d779.png-243.5kB][15]

# 11、设置软件选择 (SOFTWARE SELECTION)
>（1）选择SOFTWARE SELECTION
![image_1g3vi788118rk5kcqse49o1kt6m.png-144.1kB][16]

# 12、默认为最小安装，不带用户图形界面的，贷GUI的服务器是带桌面的 
![image_1g3vibelpqkj1llv8nkh8nsq13.png-224.5kB][17]

# 13、设置安装位置 (INSTALLATION DESTINATION)
> 
（1）选择INSTALLATION DESTINATION
（2）点选 我要配置分区，然后再点击“完成”
（3）更改模式，标准分区，点击“+”按钮添加分区
（4）添加 /boot分区，大小300MB，添加挂载点
（5）添加 swap分区，一般情况是物理内存的2倍大小，用于物理内存不足时使用，但可能造成系统不稳定，所以看情况，可以设置小一点，甚至设置为0MB，这里我设置为512MB，添加挂载点
（6）增加根分区，不填写大小，即默认剩余的空间都给根分区，添加挂载点，点击完成，并点击接受更改
![image_1g3viol43o1fifo1co5197c1n8l1g.png-136.5kB][18]
![image_1g3vipqfd16761sqv1vaf1uqjeu820.png-144kB][19]

# 14、点击开始安装
![image_1g3viqvcv131h1qsn1sf01dbt1cle2d.png-149.6kB][20]
# 15、设置root密码并等待安装完成，然后点击“重启”
![image_1g3vj8ob41gep84v1ct71p5q16u52q.png-105.2kB][21]



  [1]: http://static.zybuluo.com/corn/b0ibtdgpexf7khc8qco9vgre/image_1g3vgjhui1ughp03lk3o1s1mck9.png
  [2]: http://static.zybuluo.com/corn/8h1df1n4jg15e7olkqxg17s4/image_1g3vgkh19128qc071clp1d91ke613.png
  [3]: http://static.zybuluo.com/corn/snt7y0562x8zub7pt8z4zl53/image_1g3vglfm5mcoqn3nku1uab5f9.png
  [4]: http://static.zybuluo.com/corn/etmrvz7g75gbsyw14ji6t0v9/image_1g3vgmn5g1e31s9m1c9nsft17v4m.png
  [5]: http://static.zybuluo.com/corn/tibkg6i9i35x6rxgngvkmvkr/image_1g3vgogif1qfe1o7lbgf8ilkcv13.png
  [6]: http://static.zybuluo.com/corn/t4w7usemap7xbvgrhyni8sny/image_1g3vgu61h1ph5qtn14fihgc12ae1g.png
  [7]: http://static.zybuluo.com/corn/4dq0n96uclf57d8gw8lhlj96/image_1g3vh03c21dalg1k1rj84bu823.png
  [8]: http://static.zybuluo.com/corn/weujrf58mhrj2enxcdwfugcl/image_1g3vh12fs12501hkatqgmnv1t342g.png
  [9]: http://static.zybuluo.com/corn/npruaq26jc0r3chdgmull7mb/image_1g3vh36d41k081qa4kn1omrsn72t.png
  [10]: http://static.zybuluo.com/corn/notwp20p8mkykji0zg7ydcoj/image_1g3vh8es71bs84ig317qa24m3a.png
  [11]: http://static.zybuluo.com/corn/bj5dixxtx3viq0i3ycyui34m/image_1g3vhe53sio11asvj7k1u0e1hct3q.png
  [12]: http://static.zybuluo.com/corn/me1yfpku71n0nt9zm6juqgah/image_1g3vhipep1elc17gmqpt1rdku6o4n.png
  [13]: http://static.zybuluo.com/corn/2x4v009nk73yooi2w0f1hmri/image_1g3vhurmm8dafcn1ih42mn1afv9.png
  [14]: http://static.zybuluo.com/corn/j93mf3ef6l19u1ct8wbdvhkl/image_1g3vi0jl5op11m3c1q0qm93paj13.png
  [15]: http://static.zybuluo.com/corn/pyn41c0ji30k2tlb2ee1wmef/image_1g3vi5ki0b1p1dst9geo481d779.png
  [16]: http://static.zybuluo.com/corn/ed80uvtjrnkixh8z97rn31hs/image_1g3vi788118rk5kcqse49o1kt6m.png
  [17]: http://static.zybuluo.com/corn/thes5ak2f104muk96juqkxbw/image_1g3vibelpqkj1llv8nkh8nsq13.png
  [18]: http://static.zybuluo.com/corn/lgyf01vs3ifckftvrfnlo7y2/image_1g3viol43o1fifo1co5197c1n8l1g.png
  [19]: http://static.zybuluo.com/corn/2k8rc0nahsu3q1hbvnjkq67e/image_1g3vipqfd16761sqv1vaf1uqjeu820.png
  [20]: http://static.zybuluo.com/corn/9pzs7c0qi3yiamee3c1ivk97/image_1g3viqvcv131h1qsn1sf01dbt1cle2d.png
  [21]: http://static.zybuluo.com/corn/d33paz1delqasl3ffqm41mil/image_1g3vj8ob41gep84v1ct71p5q16u52q.png