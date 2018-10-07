# biji
&ensp;&ensp;&ensp;&ensp;通过对计算机一段的时间的学习，认识到了什么是linux，它主要是为了让服务器更好运作，是人和服务器沟通的一种工具。非x86的服务器稳定性好，但是价格贵。相对来说x86的就好的多了，而机架式的服务器基本就是主流了。 机架式（u=1.75英寸=4.5厘米1u插槽少，硬件少，
价格便宜，性能差，2u是主流十厘米。4u价格贵）。宽度是19英寸前后长度有600mm800mm1000m（买1000mm的通用）。
&ensp;&ensp;&ensp;&ensp;下面来说说linux, liunx动态库用so结尾的，静态用.a后缀的，库相当于基本元素（相当于自然界中分子，原子）。ldd命令可以查看当前文件调用的库。工作原理：用户（app)通过调用库(libary)中间有api，通过库调用系统调用syetem  call，系统调用再去调用内核(kernel),内核再去跟硬件打交道（hardware) 
哲学思想
1一切都是一个文件
2小型，单一用途的程序
3链接程序  编脚本
4避免令人困惑的界面（图形界面不可靠）
5配置数据都放在文件中，控制性好




&ensp;&ensp;&ensp;&ensp;1切换图形界面只有管理root才可以，普通用户不行
1 init3切换字符界面  init 5切换到图形界面  startx切换不需要登录  ，runlever可以看模式 init 6是重启  init0是关机命令  Poweroff （关机并断电）   halt在centos7是关机不断电
3生产中除非必要，不要登录root  ,如果需要在登录root   
4 如果判断用户  命令id-u  ID为0是管理员    终端（terminal)  gui  图形   cli  字符界面
5看看硬件，配置  看环境，
6shell是命令解释器   不同shell类型语法是不一样    工作在应用程序和操作系统之间    默认是bash类型      nolgin   系统用的shell类型
7内部命令是shell类型自带bash中带的。系统中很多内部命令都备用一个外部命令，万一内部命令不支持，可以用外部命令。外部命令会表现一个个文件，能看到路径的都是外部命令
8当需要找外部命令时时经过变量echo  $pATH来找的，当找到外部命令的路径他就会记录在内存里，这个过程叫HASH。alias----内部---  hash表（记录的外部命令路径）-----$PATH对应 的路径进行搜索------命令找不到  。       缓存将刚用过的数据放到内存中，下次用数据不需要从硬盘找，直接内存取出。
9   alias  +别名=cmd     临时的，如果想用得存到文件里    放到内存里的才会生效，要保存放到磁盘里    
10   命令的格式：命令+选项+参数    选项分长短，命令可以写到一起用分号隔开，可以一起执行。
11 如果用screen   做备份即使网断了，他也会继续执行，不会导致执行失败，支持多个人共联一台
换行和回车是两码事，换行是另起一行开始，回车是把光标移到行首。
2linux里的回车不换行  wordwos 的回车代表换行  加回车
3强引用  是单引号，不识别，放什么就显示什么。 双引号是弱引用，识别里面的变量，命令不能识别。反向单引号既能识别里面的变量和命令（通常命令调用命令）。
4ASCll编码表   128位      oct八进制    dec十进制   hex十六进制
5unicode编码方案  utf- 8主流的，基本全部都用。


获取帮助的重要性，如果能自己解决，最好不要找别人。 因为它是一种能力的体现（man,info)


block  是块设备（1k,2K）   char 是字符设备   etc 管理设备配置文件   home用户 的家目录      run运行中的数据   bin 普通用户的工具   sbin  管理员的工具   var/log  日志 变化的数据        proc  进程内存中的数据       sys硬件相关的内容   Lib64  是放库的     
  boot 放引导启动相关数据     dev设备比如硬盘和光盘    tmp临时文件        usr 第二层的根    
大小写敏感是由文件系统决定的，如果是传统linux系统是敏感的

绝对路径从根开始描述     相对路径是已经在当前目录里，直接写文件名就可以了    文件的上一级叫父目录   两个点表示相对路径法 表示当前目录的父目录       一个点表示当前目录        基名就是文件本身      目录名 就是它所在的文件名
数字文件排在字母前面  小写字母排在大写字母前面         mtime修改时间  atime读时间  ctime元数据的更改时间       如果访问的是快捷方式加不加/不一样   加/表示访问的是软连接所指的文件夹  不加/表示访问软连接本身


centos7关掉防火墙的命令systemctl stop firewalld;systemctl disable firewalld开机不启动
centos6关掉防火墙的命令service iptables stop；chkconfig iptables
‘stat （anaconda-ks.cfg）文件’可以看文件的修改时间，读时间，
‘ll --time=atime anaconda-ks.cfg’看文件的读时间
‘ll anaconda-ks.cfg’文件的修改时间
‘ll --time=ctime anaconda-ks.cfg’文件的状态更改时间
‘cat anaconda-ks.cfg’表示看文件。读时间会更改
‘touch anaconda-ks.cfg’只是对文件的时间进行刷新，对文件内容不做修改
‘touch /data/abc’touch可以创建空文件，例如‘abc’
‘touch `date +%F`.log’可以生成一个带年月日的文件。 date表示时间 F表示年月日 反向单引号可以执行里面的命令，
‘touch -t 201910200830.20（2018-09-25.log）文件’-t表示修改文件的时间戳，只修改看文件的时间和读文件的时间
‘touch -c fl’-c表示只是刷新时间戳，不创建新文件
‘touch f{1..100}’创建f1到f100个文件，用大括号
‘ll f[0-10]’中括号里的表示一个字符，10只代表0或1，不代表10  中括号里不能用点，大括号才可以。
Cp命令：
cp  --help’cp的帮助，它是外部命令。
‘cp /etc/fstab（一个源文件）  /data/fstab.bak’把目标源文件fstab放到data下fstab.bak文件里并且改名，内容进行了复制属性可能发生了变化。Fstab.bak文件是不存在的  cp的第一种语法。  如果加‘-f’表示强制删除原文件，覆盖。Root的cp 用的是别名，担心权限太大误删除会提示，如果不想提示前面加‘\’。普通用户不会提示，如果想要提示加‘-i’如果担心误覆盖，加‘--backup’它会自动加备份。
‘cp /etc/fstab（源文件） /etc/profile（源文件）   .（当前目录下）’表示把多个文件复制到当前文件下生成子目录，不能放到一个文件里
‘cp -t /data（当前文件夹） /etc/bashrc（源文件）  /etc/motd（源文件）’当前文件在前面必须加-t
‘cp -r /etc/sysconfig（文件夹）  /data/（不存在）’如果复制文件夹必须加‘-r’如果不存在，它会创建一个相同名字的文件并且生成当前目录的一个子目录。递归是进到每一个子目录里进行搜索和处理。
‘cp -r /etc/sysconfig（文件夹）  /data/sysbang（文件夹）’会改成当前文件夹的名字，进行复制
‘cp -r /etc/sysconfig  /data/sysbang’如果在执行一次cp命令，他会成为当前目录下的一个子目录。
‘-d’cp命令如果加‘-d’如果这个文件是个软连接，它只复制软连接，而不复制文件本身
‘-a’命令中如果加‘-a’ 它会原封不动的把文件复制过来（时间，属性）
‘-av’如果文件过大，加上‘v’，可以看到复制过程，以免产生误操作。
Cp命令只能拷贝普通文件，如果是设备文件必须加‘-a’以免数据丢失
‘-u’f1去覆盖f2，如果f2的时间，属性比f1新，它是不会覆盖的。主要用于设备更新。
文件名放在目录里     空间被用光了有可能节点编号被用光了 或是内存不够了     
‘>’它可以创造空文件，如果本身这个文件存在，它会清空这个文件，重新创造。最好用touch‘>>’两个大于号也能创建文件，
如果这个文件本身存在，它不会创建，如果没有这个文件，它会创建。
‘tree  -L 1（变量层数）  /etc’只显示目录下的一层  ‘-d’只列出文件夹只显示目录  ‘mkdir dir1’mkdir是创建文件夹  ‘tree –p /etc/rc*’加上‘-p（大写）’列出etc下所有以rc开头的文件
2.‘mkdir dir1/dir2/dir3 -p’加上‘-p’会自动生成上级没有的文件‘v’如果在p后面加上v可以看到过程。
3.’rmdir  d1/d2/d3/ -p’加上‘-p’它会从底向上 删除，一级一级删。（只能删空目录）
centos7的挂在点节点编号是64   centos6挂载点的节点编号是2
硬连接对一个文件起多个名字
软连接指向的是文件名  原始文件一般路径用相对路径，相对路径一定相对于软连接的相对路径
硬连接和软连接：
1不是同一个文件硬连接是 软连接不是
2软连接可以跨分区
3硬连接增长连接数
4节点编号硬连接相同
5原始文件删除硬连接不受影响  
6原始文件大小不一样  软连接的大小是路径大小
7硬连接不支持目录
8相对路径写法一样  
如果两个人要创建一个小组
第一步  先建立文件夹 mkdir   f1  
第二步  建立组  把用户1  用户2加到组里    groupadd  webs(组）     gpasswd  -a  用户1(用户2） webs           查看一下 groupmems   -l  -g  webs  
第三步把f1的主组设置成webs    chgrp  webs  f1/          设置权限 chmod  770     f1/
第四步把目录设置成sgid格式   以后在目录下创建文件，所创建的文件的所属组都将是目录的所属组   chmod     g+s        数字法表示  chmod  2770
