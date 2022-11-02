[toc]
# Linux常见命令
#### 快捷键

复制：Ctrl+insert  粘贴：Shift+insert
中止：Ctrl+c

文件传入服务器：
右键root，选择Connect SFTP Session
put 路径即可，例如put F:/freecplus_20200926.tgz
正常操作是Linux目录，前面加个l表示本地目录
get 路径，从服务区传出

解压：
tar zxvf 目录
例如tar zxvf /root/freecplus_20200926.tgz

1、开机
物理机服务器：按下电源开关，就像Windows开机一样。

本地虚拟机：在VMware中点击“开启此虚拟机”。

2、重启和关机
重启和关机需要系统管理员用户权限。

1）重启

init 6 或 reboot

2）关机

init 0 或 halt

如果没有执行关机命令，强制断电或关闭本地虚拟机的窗口，会导致Linux操作系统文件的损坏，严重的可能导致系统无法正常启动。

3、清屏
clear

清除当前屏幕上显示的内容。

4、查看服务器的ip地址
ip addr

![](https://freecplus.net/runoobFiles/ueditor/image/20200502/1588381749794021248.png)

上图中，框中显示的就是IP地址。

5、时间操作
普通用户可以查看时间，但设置时区和时间要系统管理员用户登录 。

1）查看时间。

date

2）设置时区为中国上海时间（注意不是北京时间）。

cp /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime

3）设置时间。

date -s "yyyy-mm-dd hh:mi:ss"

例如：date -s "2020-01-02 12:35:28"

6、目录和文件
文件系统是像一棵树，树干是/（根）目录，树枝是子目录，树枝后面还有树枝（子目录中还有子目录），树枝最后是树叶，目录的最后是文件。

![](https://freecplus.net/runoobFiles/ueditor/image/20200502/1588381769799018485.png)

严谨的说，文件名是由目录+文件名组成的。

对于目录和文件，有一些约定的表述，我们以/usr/etc/readme.txt为例。

1）全路径文件名包含了完整的目录名和文件名，即/usr/etc/readme.txt，还有一个称呼是“绝对路径文件名”。

2）readme.txt是文件名，它在/usr/etc目录中。

3）目录和文件的绝对路径是从根（/）算起，在任何时候都不会有岐义。

4）登录Linux后，一定处在目录树的某个目录中，这个目录称之为当前工作目录，简称当前目录。

5）目录和文件的相对路径是从当前工作目录算起，如果当前工作目录是/usr，etc/readme.txt等同于/usr/etc/readme.txt；如果当前工作目录是/usr/etc，readme.txt等同于/usr/etc/readme.txt。

6）用Linux的命令操作目录和文件的时候，采用绝对路径和相对路径都可以。

7）一个圆点.表示当前工作目录；

8）两个圆点..表示当前工作目录的上一级目录。

理解绝对路径和相对路径的概念非常重要，在日常操作中，绝对路径和相对路径会同时使用，但是程序员在编写的程序中极少使用相对路径。

7、查看当前工作目录
pwd

![](https://freecplus.net/runoobFiles/ueditor/image/20200502/1588381788814047040.png)

8、改变当前工作目录

cd 目录名

示例：

1）进入/tmp目录

cd /tmp

2）进入上一级目录

cd ..

3）进入用户的主目录

cd

9、列出目录和文件信息
ls [-lt] 目录或文件名

ls是list的缩写，通过ls 命令不仅可以查看目录和文件信息，还可以目录和文件权限、大小、主人和组等信息。

选项-l列出目录和文件的详细信息。

选项-lt列出目录和文件的详细信息，按时间降序显示。

示例：

1）列出当前工作目录下全部的目录和文件名信息。

ls

![](https://freecplus.net/runoobFiles/ueditor/image/20200502/1588381806720060844.png)

2）列出当前工作目录下全部的目录和文件名详细的信息。

ls -l

![](https://freecplus.net/runoobFiles/ueditor/image/20200502/1588381820246080796.png)

3）列出/tmp目录下全部的目录和文件。

ls /tmp

![](https://freecplus.net/runoobFiles/ueditor/image/20200502/1588381833896042309.png)

4）正则表达式

正则表达式又称规则表达式、通配符，目录和文件名都支持正则表达式，正则表达式的规则比较多，在这里我只介绍最常用的两种：星号“*”和问号“?”。

星号“*”：匹配任意数量的字符。

问号“?”：匹配一个的字符。

5）列出/tmp目录下以匹配exp*.dmp的目录和文件。

ls /tmp/exp*.dmp

![](https://freecplus.net/runoobFiles/ueditor/image/20200502/1588381852797003207.png)

6）列出/tmp目录下匹配*.log的目录和文件，按时间降序显示。

ls /tmp/*.log

![](https://freecplus.net/runoobFiles/ueditor/image/20200502/1588381862968040531.png)

10、创建目录
mkdir 目录名

示例：

1）在当前工作目录下创建aaa目录。

mkdir aaa

2）在当前工作目录的aaa目录下创建bbb目录。

mkdir aaa/bbb

3）创建/tmp/aaa目录。

mkdir /tmp/aaa

11、删除目录和文件
rm [-rf] 目录或文件列表

选项-r可以删除目录，如果没有-r只能删除文件。

选项-f表示强制删除，不需要确认。

目录和文件列表中间用空格分隔。

示例：

1）删除当前工作目录下匹配*.log的文件。

rm *.log

2）强制删除当前工作目录下匹配*.log的文件。

rm -f *.log

3）删除/tmp/aaa目录和文件。

rm -r /tmp/aaa

4）强制删除/tmp目录下匹配exp*的全部目录和文件。

rm -rf /tmp/exp*

5）强制删除当前工作目录下的book和book.c文件

rm -rf book book.c

12、移动目录和文件
mv 旧目录或文件名 新目录或文件名

如果第二个参数是已经存在的目录，则把第一个参数（旧目录或文件名）移动到该目录中。

示例：

1）把当前工作目录中的book.c文件重命名为book1.c

mv book.c book1.c

2）如果/tmp/test3是一个已经存在的目录，以下命令将把当前工作目录下的book.c文件移动到/tmp/test3目录中。

mv book.c /tmp/test3

3）如果/tmp/test3目录不存在，以下命令将把当前工作目录下的book.c文件改名为/tmp/test3。

mv book.c /tmp/test3

13、复制目录和文件
cp [-r] 旧目录或文件名 新目录或文件名

选项-r可以复制目录，如果没有选项-r只能复制文件。

示例：

1）把当前工作目录下的book1.c文件复制为book2.c

cp book1.c book2.c

2）把当前工作目录下的aaa目录复制为bbb

cp -r aaa bbb

3）把当前工作目录下的book1.c文件复制为/tmp/book1.c

cp book1.c /tmp/book1.c

cp book1.c /tmp/.

以上两个命令的效果相同。

4）把当前工作目录下的aaa目录复制为/tmp/aaa

cp -r aaa /tmp/aaa

cp -r aaa /tmp/.

以上两个命令的效果相同。

14、打包压缩和解包解压
tar命令用来打包压缩和解包解压文件，类似windows的winrar工具。

打包压缩的语法：

tar zcvf 压缩包文件名 目录或文件名列表

示例：

1）把当前工作目录的aaa、bbb和ccc目录打包压缩成123.tgz文件。

tar zcvf 123.tgz aaa bbb ccc

2）把/home/oracle/aaa、/home/oracle/bbb和/home/oracle/ccc目录打包压缩成/tmp/123.tgz文件。

tar zcvf /tmp/123.tgz /home/oracle/aaa /home/oracle/bbb /home/oracle/ccc

解包解压的语法：

tar zxvf压缩包文件名

示例：

1）把/tmp/123.tgz压缩包文件在当前工作目录下解压。

tar zxvf /tmp/123.tgz

2）把/tmp/123.tgz压缩包文件在/tmp/aaa目录下解压。

cd /tmp/aaa

tar zxvf /tmp/123.tgz

注意：

1）用tar命令打包和解包的目录和文件没有绝对路径的说法，都成了相对的，在包中相对的。

2）用tar命令打包的文件，用winrar可以解开。

3）在Linux系统中，还有其它的打包压缩和解包解压命令，例如zip/unzip和gzip/gunzip。

15、判断网络是否连通
Windows系统：

ping -n 包的个数 ip地址或域名

Linux系统：

ping -c 包的个数 ip地址或域名

ping用于确定本地主机是否能与另一台主机成功交换数据包，判断网络是否通畅。

127.0.0.1是指本地的ip地址，ping 127.0.0.1总是可以通的。

示例：

1）向本地主机（127.0.0.1）ping五个包。

ping -c 5 127.0.0.1

![](https://freecplus.net/runoobFiles/ueditor/image/20200502/1588381889541051193.png)

2）向新浪（www.sina.com.cn）的服务器ping五个包。

![](https://freecplus.net/runoobFiles/ueditor/image/20200502/1588381901421056289.png)

新浪的服务器是可以ping通的。

3）向谷歌（www.google.com）的服务器ping五个包。

![](https://freecplus.net/runoobFiles/ueditor/image/20200502/1588381919169033167.png)

谷歌的服务器是ping不通的。

16、显示文本文件的内容
显示文本文件的内容有三个命令：cat、more和tail。

1）cat命令

cat 文件名

cat命令一次显示整个文件的内容。

cat book1.c

![](https://freecplus.net/runoobFiles/ueditor/image/20200502/1588381934195037062.png)

2）more命令

more 文件名

为了方便阅读，more命令分页显示文件的内容，按空格键显示下一页，按b键显上一页，按q键退出。

3）tail命令

tail -f 文件名

tail -f用于显示文本文件的最后几行，如果文件的内容有增加，就实时的刷新。对程序员来说，tail -f极其重要，可以动态显示后台服务程序的日志，用于调试和跟踪程序的运行。

17、统计文本文件的行数、单词数和字节数
wc 文件名

示例：

1）统计当前工作目录处book2*.c文件的行数、单词数和字节数。

wc book2*.c

![](https://freecplus.net/runoobFiles/ueditor/image/20200502/1588381947436056980.png)

18、搜索文件中的内容
grep "内容" 文件名

注意，如果内容中没有空格等特殊字符，可以不用双引号括起来。

示例：

1）在*.c文件中搜索max

grep max *.c

![](https://freecplus.net/runoobFiles/ueditor/image/20200502/1588381962891093074.png)

19、搜索文件
find 目录名 -name 文件名 -print

参数说明：

目录名：待搜索的目录，搜索文件的时候，除了这个目录名，还包括它的各级子目录。

文件名：待搜索的文件名匹配的规则。

示例：

1）从/tmp目录开始搜索，把全部的*.c文件显示出来。

find /tmp -name *.c -print

2）从当前工作目录开始搜索，把全部的*.c文件显示出来。

find . -name *.c -print

20、增加/删除用户组
1）增加用户组

groupadd 组名

例如：

groupadd dba

2）删除用户组

groupdel 组名

例如：

groupdel dba

21、增加/删除用户
1）增加用户

useradd -n 用户名 -g 组名 -d 用户的主目录

例如增加一个用户，用户名为wucz，属于dba组，用户的主目录是/home/wucz，各位兄弟，wucz是我的名字，您可以改为您自己的名字。

useradd  -n  wucz  -g  dba  -d  /home/wucz

2）删除用户

userdel 用户名

例如删除wucz用户。

userdel wucz


22、修改用户的密码
passwd [用户名]

修改用户的密码，按提示两次输入新密码，如果两次输入的密码相同就修改成功。

普通用户只能修改自己的密码，只输入passwd就可以了，不能指定用户名。

系统管理员可以修改任何用户的密码，passwd后需要指定用户名。

23、切换用户
在命令提示符下输入：su - root ，然后按提示输入root的密码后将切换到root用户。

从root用户切换到其它普通用户不需要输入密码，从普通用户切换到任何用户都需要输入密码。

![](https://freecplus.net/runoobFiles/ueditor/image/20200502/1588381981948067367.png)

24、修改目录和文件的主人和组
chown [-R] 用户名:组名 目录或文件名列表

chown将目录或文件的拥有者修改为参数指定的用户名和组，目录或文件名列表用空格分隔。

-R 选项表示处理各及子目录。

示例：

1）把/oracle/home和/oracle/base及其子目录的主人改为oracle，组改为dba。

chown -R oracle:dba /oracle/home /oracle/base

25、查看系统磁盘空间
df [-h] [-T]

选项-h 以方便阅读的方式显示信息。

选项-T 列出文件系统类型。

示例：

![](https://freecplus.net/runoobFiles/ueditor/image/20200502/1588382003881041555.png)

![](https://freecplus.net/runoobFiles/ueditor/image/20200502/1588382012509027703.png)

# vi常见命令

1、创建/打开文件
vi 文件名

打开一个文件，如果文件不存在，就创建它。

示例：

vi book.c

2、vi的三种模式
vi 有三种模式，命令行模式、插入模式和替换模式，在命令行模式下，任何键盘输入都是命令，在插入模式和替换模式下，键盘输入的才是字符。

插入模式和替换模式也合称为编辑模式。

3、vi的常用命令
Esc      从编辑模式切换到命令行模式。

 

i    在光标所在位置前面开始插入。

a    在光标所在的位置后面开始插入。

o   在光标所在位置行的下面插入空白行。

O   在光标所在位置行的上面插入空白行。

I    在光标所在位置行的行首开始插入。

A   在光标所在位置行的行末开始插入。

 

k    类似方向键上。

j    类似方向键下。

h   类似方向键左。

l    类是方向键右。

 

Ctrl+u  向上翻半页。

Ctrl+d  向下翻页。

 


Ctrl+g      显示光标所在位置的行号和文件的总行数。



nG 光标跳到文件的第n行行首。

G   光标跳到文件最后一行。

:5回车   光标跳到第5行。

:n回车   光标跳到第n行。

 

0    光标跳到当前行的行首。

$    光标跳到当前行的行尾。

 

w    光标跳到下个单词的开头。

b    光标跳到上个单词的开头。

e   光标跳到本单词的尾部。

 

x     每按一次，删除光标所在位置的一个字符。

nx   如"3x"表示删除光标所在位置开始的3个字符。

dw  删除光标所在位置到本单词结尾的字符。

D   删除本行光标所在位置后面全部的内容。

 

dd   删除光标所在位置的一行。

ndd  如"3dd"表示删除光标所在位置开始的3行。

 

yy   将光标所在位置的一行复制到缓冲区。

nyy 将光标所在位置的n行复制到缓冲区。

p    将缓冲区里的内容粘贴到光标所在位置。

 

r     替换光标所在位置的一个字符 replace。

R   从光标所在位置开始替换，直到按下"Esc"。

cw 从光标所在位置开始替换单词，直到按下"Esc"。

 

u   撤销命令，可多次撤销。

 

J   把当前行的下一行接到当前行的尾部。

 

/abcd  在当前打开的文件中查找“abcd”文本内容。

n      查找下一个。

N      查找上一下。

 

.    重复执行上一次执行的vi命令。

 

~   对光标当前所在的位置的字符进行大小写转换。

 

列操作

Ctrl+V   光标上或下  大写的I  输入内容  Esc

 

:w回车   存盘。

:w!回车   强制存盘。

:wq回车 存盘退出。

:x回车    存盘退出。

:q回车  不存盘退出。

:q!回车  不存盘强制退出。

 

:g/aaaaaaaaa/s//bbbbbb/g回车    把文件中全部的aaaaaaaaa替换成bbbbbb。

 

Ctl+insert   复制鼠标选中的文本，相当于Ctl+c。

Shift+insert 输出鼠标选中的文本，相当于Ctl+v。

以上两个命令在windows和UNIX中是通用的。

# 环境变量

一、环境变量的概念
1、环境变量的含义
程序（操作系统命令和应用程序）的执行都需要运行环境，这个环境是由多个环境变量组成的。

2、环境变量的分类
1）按生效的范围分类。

系统环境变量：公共的，对全部的用户都生效。

用户环境变量：用户私有的、自定义的个性化设置，只对该用户生效。

2）按生存周期分类。

永久环境变量：在环境变量脚本文件中配置，用户每次登录时会自动执行这些脚本，相当于永久生效。

临时环境变量：使用时在Shell中临时定义，退出Shell后失效。

3、Linux环境变量
Linux环境变量也称之为Shell环境量变，以下划线和字母打头，由下划线、字母（区分大小写）和数字组成，习惯上使用大写字母，例如PATH、HOSTNAME、LANG等。

二、常用的环境变量
1、查看环境变量
1）env命令

在Shell下，用env命令查看当前用户全部的环境变量。

![](https://freecplus.net/runoobFiles/ueditor/image/20200713/1594626412004083135.png)

上图只截取了部分环境变量，并非全部。

用env命令的时候，满屏显示了很多环境变量，不方便查看，可以用grep筛选。

env|grep 环境变量名

例如查看环境变量名中包含PATH的环境变量。

env|grep PATH

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584493962788023266.png)

2）echo命令

echo $环境变量名

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584493976176020727.png)

注意，符号$不能缺少，这是语法规定。

2、常用的环境变量
1）PATH

可执行程序的搜索目录，可执行程序包括Linux系统命令和用户的应用程序，PATH变量的具体用法本文后面的章节中有详细的介绍。

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584493993156031998.png)

2）LANG

Linux系统的语言、地区、字符集，LANG变量的具体用法本文后面的章节中有详细的介绍。

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584494006552051021.png)

3）HOSTNAME

服务器的主机名。

4）SHELL

用户当前使用的Shell解析器。

5）HISTSIZE

保存历史命令的数目。

6）USER

当前登录用户的用户名。

7）HOME

当前登录用户的主目录。

8）PWD

当前工作目录。

9）LD_LIBRARY_PATH

C/C++语言动态链接库文件搜索的目录，它不是Linux缺省的环境变量，但对C/C++程序员来说非常重要，具体用法本文后面的章节中有详细的介绍。

10）CLASSPATH

JAVA语言库文件搜索的目录，它也不是Linux缺省的环境变量，但对JAVA程序员来说非常重要，具体用法本文后面的章节中有详细的介绍。

三、设置环境量

变量名='值'
export 变量名
或

export 变量名='值'
如果环境变量的值没有空格等特殊符号，可以不用单引号包含。

示例：

export ORACLE_HOME=/oracle/home
export ORACLE_BASE=/oracle/base
export ORACLE_SID=snorcl11g
export NLS_LANG='Simplified Chinese_China.ZHS16GBK'
export PATH=$PATH:$HOME/bin:$ORACLE_HOME/bin:.
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$ORACLE_HOME/lib:.
采用export设置的环境变量，在退出Shell后就会失效，下次登录时需要重新设置。如果希望环境变量永久生效，需要在登录脚本文件中配置。

1、系统环境变量
系统环境变量对全部的用户生效，设置系统环境变量有三种方法。

1）在/etc/profile文件中设置。

用户登录时执行/etc/profile文件中设置系统的环境变量。但是，Linux不建议在/etc/profile文件中设置系统环境变量。

2）在/etc/profile.d目录中增加环境变量脚本文件，这是Linux推荐的方法。

/etc/profile在每次启动时会执行 /etc/profile.d下全部的脚本文件。/etc/profile.d比/etc/profile好维护，不想要什么变量直接删除 /etc/profile.d下对应的 shell 脚本即可。

/etc/profile.d目录下有很多脚本文件，例如：

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584494069551087486.png)

在以上示例中，/etc/profile.d目录中的oracle.sh是Oracle数据库的环境变量配置文件，内容如下：

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584494082197084532.png)

3）在/etc/bashrc文件中设置环境变量。

该文件配置的环境变量将会影响全部用户使用的bash shell。但是，Linux也不建议在/etc/bashrc文件中设置系统环境变量。

2、用户环境变量
用户环境变量只对当前用户生效，设置用户环境变量也有多种方法。

在用户的主目录，有几个特别的文件，用ls是看不见的，用ls .bash_*可以看见。

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584494097502047389.png)

1）.bash_profile（推荐首选）

当用户登录时执行，每个用户都可以使用该文件来配置专属于自己的环境变量。

2）.bashrc

当用户登录时以及每次打开新的Shell时该文件都将被读取，不推荐在里面配置用户专用的环境变量，因为每开一个Shell，该文件都会被读取一次，效率肯定受影响。

3）.bash_logout

当每次退出系统（退出bash shell）时执行该文件。

4）.bash_history

保存了当前用户使用过的历史命令。

3、环境变量脚本文件的执行顺序
环境变量脚本文件的执行顺序如下：

/etc/profile->/etc/profile.d->/etc/bashrc->用户的.bash_profile->用户的.bashrc

同名的环境变量，如果在多个脚本中有配置，以最后执行的脚本中的配置为准。

还有一个问题需要注意，在/etc/profile中执行了/etc/profile.d的脚本，代码如下：

for i in /etc/profile.d/*.sh ; do
    if [ -r "$i" ]; then
        if [ "${-#*i}" != "$-" ]; then
            . "$i"
        else
            . "$i" >/dev/null
        fi
    fi
done
所以，/etc/profile.d和/etc/profile的执行顺序还要看代码怎么写。

四、重要环境变量的详解
1、PATH环境变量
可执行程序的搜索目录，可执行程序包括Linux系统命令和用户的应用程序。如果可执行程序的目录不在PATH指定的目录中，执行时需要指定目录。

1）PATH环境变量存放的是目录列表，目录之间用冒号:分隔，最后的圆点.表示当前目录。

export PATH=目录1:目录2:目录3:......目录n:.

2）PATH缺省包含了Linux系统命令所在的目录（/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin），如果不包含这些目录，Linux的常用命令也无法执行（要输入绝对路径才能执行）。

示例：
![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584494134036053965.png)

3）在用户的.bash_profile文件中，会对PATH进行扩充，如下：

export PATH=$PATH:$HOME/bin

4）如果PATH变量中没有包含圆点.，执行当前目录下的程序需要加./或使用绝对路径。

示例：

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584494150347058546.png)

2、LANG环境变量
LANG环境变量存放的是Linux系统的语言、地区、字符集，它不需要系统管理员手工设置，/etc/profile会调用/etc/profile.d/lang.sh脚本完成对LANG的设置。

CentOS6.x 字符集配置文件在/etc/syscconfig/i18n文件中。

CentOS7.x 字符集配置文件在/etc/locale.conf文件中，内容如下：

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584494165241004525.png)

3、LD_LIBRARY_PATH环境变量
C/C++ 语言动态链接库文件搜索的目录，它不是Linux缺省的环境变量，但对C/C++程序员来说非常重要。

LD_LIBRARY_PATH环境变量存放的也是目录列表，目录之间用冒号:分隔，最后的圆点.表示当前目录，与PATH的格式相同。

export LD_LIBRARY_PATH=目录1:目录2:目录3:......目录n:.

4、CLASSPATH
JAVA语言库文件搜索的目录，它也不是Linux缺省的环境变量，但对JAVA程序员来说非常重要。

CLASSPATH环境变量存放的也是目录列表，目录之间用冒号:分隔，最后的圆点.表示当前目录，与PATH的格式相同。

五、环境变量的生效
1）在Shell下，用export设置的环境变量对当前Shell立即生效，Shell退出后失效。

2）在脚本文件中设置的环境变量不会立即生效，退出Shell后重新登录时才生效，或者用source命令让它立即生效，例如：

source /etc/profile


# 字符集
一、字符编码和字符集
计算机中处理和储存信息都是用二进制数表示的；而我们在屏幕上看到的英文、汉字等字符是二进制数转换之后的结果。通俗的说，按照某种规则将字符存储在计算机中，如'a'用97表示，称为"编码"；反之，将计算机中的二进制数解析显示出来，称为"解码"。在解码过程中，如果使用了错误的解码规则，就会产生乱码。

1、字符编码（character encoding）

字符编码是一种法则，在数字与字符之间建立的对应关系。

不同的国家有不同的字符，包含的文字、标点符号、图形符号各有不同。

常见的字符编码有ASCII，GBK，GB18030，Unicode等。

2、字符集（Character set）
字符是文字和符号的总称，字符集是字符的集合，是数字与字符的对照表。

用ASCII编码的字符集称之为ASCII字符集，用GBK编码的字符集称之为GBK字符集。

3、国际编码（Unicode）
为了解决传统的字符编码方案的局限，1994年发布了Unicode（国际编码、统一码、万国码、单一码、通用码），它是计算机科学领域里的一项业界标准，包括字符集、编码方案等。Unicode 将全世界所有的字符统一编码，再也不存在字符集不兼容和字符转换的问题。

Unicode 有以下三种编码方式：

1）UTF-8：兼容ASCII编码；拉丁文、希腊文等使用两个字节；包括汉字在内的其它常用字符使用三个字节；剩下的极少使用的字符使用四个字节。

2）UTF-16：对相对常用的60000余个字符使用两个字节进行编码，其余的使用4字节。

3）UTF-32：固定使用4个字节来表示一个字符，存在空间利用效率的问题。

二、汉字的编码
1、汉字的编码
支持汉字（简体中文）的编码有GB2312、GB13000、GBK、GB18030和Unicode（UTF-8、UTF-16、UTF-32）。

1）GB2312

仅包含大部分的常用简体汉字，但已经不能适应现在的需要。

2）GB13000

由于GB2312的局限性，国家标准化委员会制定了GB13000编码； 但由于当时的硬件和软件都已经支持了GB2312，而GB13000与GB2312完全不兼容，所以没有能够得到大范围的推广使用。

3）GBK

有了GB13000的教训，中国国家标准化委员会制定了GBK标准，并兼容了GB2312标准，同时在GB2312标准的基础上扩展了GB13000包含的字； 由于该标准有微软的支持，得到了广泛的应用。双字节表示

4）GB18030

GB18030编码比GBK又新增了几千个汉字，但由于码位不足使用了2byte与4byte混合编码方式，这给软件开发增加了难度。

5）Unicode

包含全世界所有国家需要用到的字符，是国际编码，通用性强。

2、汉字的编码选择
在操作系统和数据库中，常用的汉字编码有GBK、GB18030和Unicode，GBK和GB18030的优势是占用空间小，Unicode的优势是全球化的支持。

3、编码的转换
GBK和GB18030与Unicode编码之间需要转换，否则会出现汉字乱码。

三、设置Linux的字符集
1、查看当前系统已安装的字符集
1）locale命令用于查看当前系统全部的已安装的字符集，Linux支持的符集约800种。

locale -a 

2）查看已安装的中文字符集（只查看中国大陆的，不包括香港和台湾）

locale -a|grep zh_CN

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584494808555092817.png)

上图表示已经安装了中文字符集。

2、安装中文字符集
如果您的Linux系统没有安装中文字符集，可以用yum命令安装。

我查了一些资料，安装中文字符集软件包的方法比较多，没找到准确的说法，所以把多种方法都写了进来，以下命令用root用户执行，不会有副作用。

yum -y groupinstall chinese-support

yum -y install chinese-support

yum -y install kde-l10n-Chinese

yum -y install ibus-table-chinese-1.4.6-3.el7.noarch

安装后，执行locale -a|grep zh_CN，如果显示的内容如下，表示安装成功。

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584494898106012931.png)

3、修改字符集配置文件
CentOS6.x字符集配置文件在/etc/sysconfig/i18n文件中。

CentOS7.x字符集配置文件在/etc/locale.conf文件中，内容如下：

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584495043966060948.png)

执行以下命令或者重启系统使修改生效。

CentOS6.x

source /etc/sysconfig/i18n

CentOS7.x:

source /etc/locale.conf

四、LANG环境变量
LANG环境变量存放的是Linux系统的语言、地区、字符集，它不需要系统管理员手工设置，/etc/profile会调用/etc/profile.d/lang.sh脚本完成对LANG的设置。

五、修改客户端的字符集
客户端的字符集必须与Linux服务端一致，否则会出现乱码，以SecureCRT为例。修改会话的属性，在Appearance界面中的Character encoding下拉框中选择。

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584495062876052608.png)

六、字符集转换工具
Linux提供了iconv命令把文件内容从一种编码转换成另一种编码。

参数说明：

--list：列出iconv支持的编码列表。

-f encoding：源文件内容的编码。

-t encoding：目标文件内容的编码。 

-o file：指定输出文件。

-c：忽略输出的非法字符。

-l：列出已知的编码字符集。

-s：禁止警告信息，但不是错误信息。

--verbose：显示进度信息。

示例：

把当前目录的book1.c由gbk转换成utf-8，结果输出到/tmp/book1_utf8.c中。

iconv -f gbk -t utf-8 book1.c -o /tmp/book1_utf8.c

# 软件包的安装方法
一、rpm安装
RPM是RedHat Package Manager的缩写，由RedHat推出的软件包管理管理工具，在Fedora 、Redhat、CentOS、Mandriva、SuSE、YellowDog等主流发行版本，以及在这些版本基础上二次开发出来的发行版采用。

RPM包里面包含可执行的二进制程序，自身所带的附加文件，版本文件（软件包的依赖关系）。

1、查看系统中已安装的软件包
1）查看已安装的软件包。

rpm -q 软件包名

例如查看ftp客户端和ftp服务端软件包：

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584495321473077127.png)

2）查看软件包安装的目录和文件（包括了可执行程序、配置文件和帮助文档）。

rpm -ql 软件包名

例如查看ftp客户端：

rpm -ql ftp

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584495346991063305.png)

3）查看已安装软件包的详细信息。

rpm -qi 软件包名

例如查看ftp客户端（显示内容太多，部分截图）：

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584495386099001816.png)

4）查看已安装软件包的配置。

rpm -qc 软件包名

例如查看ftp服务端：

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584495402401048092.png)

5）查看已安装软件包所依赖的软件包及文件。

rpm -qR 软件包名

例如查看ftp客户端（显示内容太多，部分截图）：

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584495427557029080.png)

2、查看软件包的安装文件
安装包文件的后缀是.rpm，以CentOS7为例，系统安装的光盘映像文件是CentOS-7-x86_64-DVD-1908.iso，解开后在Packages目录中有软件包的安装文件，如下：

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584495451614069285.png)

接下来以ftp的客户端安装包文件ftp-0.17-67.el7.x86_64.rpm为例来介绍安装包文件的查看方法。

1）查看一个软件包的安装文件的详细信息。

rpm -qpi 软件包的安装文件名

（显示内容太多，部分截图）

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584495477846021109.png)

2）查看软件包的安装文件所包含的文件。

rpm -qpl 软件安装包文件名

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584495502116091669.png)

3）查看软件包的依赖关系。

rpm -qpR 软件包的安装文件名

3、安装/升级软件包
如果待安装/升级的软件与其它的软件有依赖关系，请解决依赖关系，即先安装/升级依赖关系的软件包。如果没有解决好依赖关系，可以强制安装/升级，不推荐采用强制的方法，因为有可能导致软件不可用。

1）安装软件包。

rpm -ivh 软件包的安装文件名

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584495549511095479.png)

2）升级软件包。

rpm -Uvh 软件包的安装文件名

![](https://freecplus.net/runoobFiles/ueditor/image/20200919/1600482223183038461.png)

3）强制安装软件包。

rpm -ivh 软件包的安装文件名 --nodeps --force

4）强制升级软件包。

rpv -Uvh 软件包的安装文件名 --nodeps --force

4、删除软件包
rpm -e 软件包名

例如删除ftp客户端软件包：

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584495604529000784.png)

二、yum安装
rpm安装软件包的虽然方便，但是需要手工解决软件包的依赖关系。很多时候安装一个软件包需要安装多个其他软件包，还有不同版本的兼容性问题，很复杂。yum（Yellow dog Updater, Modified）解决了这些问题，yum是rpm的前端程序，设计的主要目的就是为了自动解决rpm的依赖关系，有以下优点：

1) 自动解决依赖关系；

2) 可以对rpm进行分组，基于组进行安装操作；

3) 引入仓库概念，支持多个仓库；

4) 配置简单。

1、yum的语法
yum [options] [command] [package ...]

options：可选参数：1）-h帮助；2）-y，当安装过程提示选择全部为yes，不需要再次确认；3）-q，不显示安装的过程。

command：待操作的命令。

package：待操作的软件包名，多个软件包之间用空格分开，支持用星号*匹配。

2、yum的常用命令
最最常用的命令加粗显示。

1）安装/升级软件包。

yum install 软件包名/软件包文件名

2）升级软件包。

yum update 软件包名

3）删除软件包。

yum remove 软件包名

4）查找软件包。

yum search 软件包名

5）列出所有可更新的软件包清单。

yum check-update

6）更新所有软件包。

yum update

7）列出所有可安装软件包的清单；

yum list

8）清除缓存。

yum clean [headers|packages|metadata|dbcache|plugins|expire-cache|all]

3、示例
1）安装/升级ftp客户端软件包。

yum -y install ftp

或

yum -y install ftp-0.17-67.el7.x86_64.rpm

2）升级ftp客户端软件包

yum -y update ftp

3）删除ftp客户端软件包。

yum -y remove ftp

# 系统服务管理

一、systemctl介绍
CentOS7启用了新的系统和服务管理器，采用systemctl命令代替了老版本的service和chkconfig。为了保持兼容性，在CentOS7中，老版本的service和chkconfig命令仍然可以使用。

systemctl命令是system（系统）和control（控制）两个单词的简写，它是一个功能强大的命令，本文只介绍与服务管理相关的用法。

systemctl命令有一点不足，就是很多命令执行后没有提示信息，例如下图：

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584495920027025227.png)

上图中，执行启动和停止服务命令后没有“服务已启动”或“服务已关闭”等提示信息，让人很不习惯。还有，start和stop各执行了两次，也没有任何提示信息，这也让人很不习惯。

二、systemctl常用命令
1、启动服务
systemctl start name.service

注意name.service的.service可以省略不写，以下两条命令的效果相同。

systemctl start vsftpd             # 启动ftp服务。

systemctl start vsftpd.service      # 启动ftp服务。

2、停止服务
systemctl stop name.service

3、重启服务
如果服务没有启动，就启动它。

systemctl restart name.service

4、查看服务是否已启动
systemctl is-active name.service

5、查看服务的状态
systemctl status name.service

示例：
![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584495948370086356.png)

Loaded：关于服务是否已经加载的信息，文件的绝对路径以及是否被启用的注释。

Active：服务是否正在运行,然后是启动时间信息。

Process：进程额外信息。

Main PID：服务主进程pid。

CGroup:Control Groups额外信息。

6、启用开机自启动服务
systemctl enable name.service

7、停用开机自启动服务
systemctl disable name.service

8、查看服务是否为开机自启动
systemctl is-enabled name.service

9、只重启正在运行中的服务
systemctl try-restart name.service

10、显示所有的服务状态
按空格键显示下一页，按q键退出。

systemctl list-units --type service --all

11、查看启动成功的服务列表
systemctl list-unit-files|grep enabled

12、查看启动失败的服务列表
systemctl --failed

13、查看所有服务的状态
按空格键显示下一页，按q键退出。

systemctl list-unit-files --type service

14、列出在指定服务之前启动的服务（依赖）
按空格键显示下一页，按q键退出。

systemctl list-dependencies --after name.service

15、列出在指定服务之后启动的服务（被依赖）
按空格键显示下一页，按q键退出。

systemctl list-dependencies --before name.service

# 自定义系统服务

CentOS 6版本的系统服务是/etc/init.d启动脚本的方式，CentOS 7采用强大的systemctl来管理系统服务，大幅提高了系统服务的运行效率，但是服务的配置和以前版本完全不同，这是很大的进步，systemctl太简单易用了。

CentOS7添加自定义系统服务的步骤如下：

1）编写自定义的系统服务脚本文件；

2）用systemctl命令把自定义的系统服务设置为开机/关机自启动/停止。

本文以Oracle数据库为例子来介绍添加自定义系统服务的知识。假设ORACLE_HOME环境变量的值是/oracle/home，各位根据自己的实际情况调整脚本的内容，把文中/oracle/home替换成您ORACLE_HOME的值。

一、编写Oracle数据库启动/重启/关闭的脚本
1、启动Oracle数据库的shell脚本
启动Oracle数据库的脚本为/oracle/home/bin/dbstart，内容如下：
sqlplus / as sysdba <<EOF
startup;
EOF
修改脚本的权限为可执行。

chmod +x /oracle/home/bin/dbstart

2、重启Oracle数据库的shell脚本
启动Oracle数据库的脚本为/oracle/home/bin/dbrestart，内容如下：

sqlplus / as sysdba <<EOF
shutdown immediate;
startup;
EOF
修改脚本的权限为可执行。

chmod +x /oracle/home/bin/dbrestart

3、关闭Oracle数据库的shell脚本
启动Oracle数据库的脚本为/oracle/home/bin/dbshut，内容如下：

sqlplus / as sysdba <<EOF
shutdown immediate;
EOF
修改脚本的权限为可执行。

chmod +x /oracle/home/bin/dbshut

二、编写自定义服务的配置文件
系统服务的启动/重启/停止由它的配置文件决定，本文把Oracle数据库的系统服务命名为oracle.service。

创建服务配置文件/usr/lib/systemd/system/oracle.service，内容如下：

[Unit]
Description=Oracle RDBMS
After=network.target
 
[Service]
Type=simple
ExecStart=/usr/bin/su - oracle -c "/oracle/home/bin/dbstart >> /tmp/oracle.log"
ExecReload=/usr/bin/su - oracle -c "/oracle/home/bin/dbrestart >> /tmp/oracle.log"
ExecStop=/usr/bin/su - oracle -c "/oracle/home/bin/dbshut >> /tmp/oracle.log"
RemainAfterExit=yes
 
[Install]
WantedBy=multi-user.target
接下来介绍服务配置文件各部分的含义。

1、Unit部分
Unit部分是启动顺序与依赖关系。

[Unit]
Description=Oracle RDBMS
After=network.target
Description字段：给出当前服务的简单描述。

Documentation字段：给出文档位置。

After字段：表示本服务应该在某服务之后启动。

Before字段：表示本服务应该在某服务之前启动。

After和Before字段只涉及启动顺序，不涉及依赖关系。设置依赖关系，需要使用Wants字段和Requires字段。

Wants字段：表示本服务与某服务之间存在“依赖”系，如果被依赖的服务启动失败或停止运行，不影响本服务的继续运行。

Requires字段，表示本服务与某服务之间存在“强依赖”系，如果被依赖的服务启动失败或停止运行，本服务也必须退出。

2、Service部分
Service部分定义如何启动/重启/停止服务。

[Service]
Type=simple
ExecStart=/usr/bin/su - oracle -c "/oracle/home/bin/dbstart >> /tmp/oracle.log"
ExecReload=/usr/bin/su - oracle -c "/oracle/home/bin/dbrestart >> /tmp/oracle.log"
ExecStop=/usr/bin/su - oracle -c "/oracle/home/bin/dbshut >> /tmp/oracle.log"
RemainAfterExit=yes
1）启动类型（Type字段）

Type字段定义启动类型。它可以设置的值如下。

simple（默认值）：ExecStart字段启动的进程为主进程。

forking：ExecStart字段将以fork()方式启动，此时父进程将会退出，子进程将成为主进程。

oneshot：类似于simple，但只执行一次，Systemd会等它执行完，才启动其他服务。

dbus：类似于simple，但会等待D-Bus信号后启动。

notify：类似于simple，启动结束后会发出通知信号，然后Systemd再启动其他服务。

idle：类似于simple，但是要等到其他任务都执行完，才会启动该服务。

2）启动服务（ExecStart字段）

启动服务时执行的命令，可以是可执行程序、系统命令或shell脚本。

3）重启服务（ExecReload字段）

重启服务时执行的命令，可以是可执行程序、系统命令或shell脚本。

4）停止服务（ExecStop字段）

停止服务时执行的命令，可以是可执行程序、系统命令或shell脚本。

5）如果RemainAfterExit字段设为yes，表示进程退出以后，服务仍然保持执行。

6）服务配置文件还可以读取环境变量参数文件，我个人认为比较麻烦，没有必要，就不介绍了，设置程序的环境变量有很多种方法，可以在脚本中配置，也可以用“su –”的方法。

3、Install部分
Install部分定义如何安装这个配置文件，即怎样做到开机启动。

[Install]
WantedBy=multi-user.target
WantedBy字段：表示该服务所在的Target。

Target的含义是服务组，表示一组服务。WantedBy=multi-user.target指的是，oracle所在的Target是multi-user.target（多用户模式）。

这个设置非常重要，因为执行systemctl enable oracle.service命令时，oracle.service会被链接到/etc/systemd/system/multi-user.target.wants目录之中，实现开机启动的功能。

4、重启行为
Service部分还有一些字段，定义了重启行为。

1）KillMode字段

KillMode字段定义Systemd如何停止sshd服务，可以设置的值如下：

control-group（默认值）：当前控制组里面的所有子进程，都会被杀掉。

process：只杀主进程。

mixed：主进程将收到SIGTERM信号，子进程收到SIGKILL信号。

none：没有进程会被杀掉，只是执行服务的stop命令。

2）Restart字段

Restart字段定义了服务程序退出后，Systemd的重启方式，可以设置的值如下：

no（默认值）：退出后不会重启。

on-success：只有正常退出时（退出状态码为0），才会重启。

on-failure：非正常退出时（退出状态码非0），包括被信号终止和超时，才会重启。

on-abnormal：只有被信号终止和超时，才会重启。

on-abort：只有在收到没有捕捉到的信号终止时，才会重启。

on-watchdog：超时退出，才会重启。

always：不管是什么退出原因，总是重启。

3）RestartSec字段。

RestartSec字段：表示Systemd重启服务之前，需要等待的秒数。

三、使用自定义的服务
1、重新加载服务配置文件
每次修改了服务配置文件后，需要执行以下命令重新加载服务的配置文件。

systemctl daemon-reload

2、启动/停止/启重oracle服务
systemctl start oracle  # 启动oracle服务。

systemctl restart oracle # 重启oracle服务。

systemctl stop oracle  # 关闭oracle服务。

3、把oracle服务设置为开机/关机自启动/停止
systemctl is-enabled oracle  # 查看oracle服务是否是开机自启动。

systemctl enable oracle  # 把oracle服务设置为开机自启动。

4、查看Oracle实例启动/停止的日志
Oracle实例启动的日志在/tmp/oracle.log文件中。

注意，只有通过systemctl启动/关闭Oracle实例和监听才会写日志，手工执行脚本不写日志

# 防火墙

一、防火墙的概念

防火墙技术是用于安全管理的软件和硬件设备，在计算机内/外网之间构建一道相对隔绝的保护屏障，以保护数据和信息安全性的一种技术。

防火墙分为网络防火墙和主机防火墙。

网络防火墙由软件和硬件组成，可以保护整个网络，价格也很贵，从几万到几十万的都有，功能非常强大，主要包括入侵检测、网络地址转换、网络操作的审计监控、强化网络安全服务等功能。

主机防火墙只有软件部分（操作系统和杀毒软件自带），用于保护本操作系统，功能比较简单，只能防范简单的攻击。

本文将介绍主机防火墙（CentOS7以上版本）的使用和配置。

二、防火墙配置
CentOS7的防火墙比CentOS6的功能更强大，配置方法和操作命令也完全不同。

CentOS7的防火墙规则既可以是端口，也可以是服务。

防火墙查看和配置以下介绍的命令，如果没有特别说明就表示需要管理员权限执行。

1、查看防火墙的命令
1）查看防火墙的版本。

firewall-cmd --version

2）查看firewall的状态。

firewall-cmd --state

3）查看firewall服务状态（普通用户可执行）。

systemctl status firewalld

4）查看防火墙全部的信息。

firewall-cmd --list-all

5）查看防火墙已开通的端口。

firewall-cmd --list-port

6）查看防火墙已开通的服务。

firewall-cmd --list-service

7）查看全部的服务列表（普通用户可执行）。

firewall-cmd --get-services

8）查看防火墙服务是否开机启动。

systemctl is-enabled firewalld

2、配置防火墙的命令
 1）启动、重启、关闭防火墙服务。

启动

systemctl start firewalld

重启

systemctl restart firewalld

关闭

systemctl stop firewalld

2）开放、移去某个端口。

开放80端口

firewall-cmd --zone=public --add-port=80/tcp --permanent

移去80端口

firewall-cmd --zone=public --remove-port=80/tcp --permanent

3）开放、移去范围端口。

开放5000-5500之间的端口

firewall-cmd --zone=public --add-port=5000-5500/tcp --permanent

移去5000-5500之间的端口

firewall-cmd --zone=public --remove-port=5000-5500/tcp --permanent

4）开放、移去服务。

开放ftp服务

firewall-cmd --zone=public --add-service=ftp --permanent

移去http服务

firewall-cmd --zone=public --remove-service=ftp --permanent

5）重新加载防火墙配置（修改配置后要重新加载防火墙配置或重启防火墙服务）。

firewall-cmd --reload

6）设置开机时启用、禁用防火墙服务。

启用服务

systemctl enable firewalld

禁用服务

systemctl disable firewalld

三、centos7以下版本
1）开放80，22，8080 端口。

/sbin/iptables -I INPUT -p tcp --dport 80 -j ACCEPT

/sbin/iptables -I INPUT -p tcp --dport 22 -j ACCEPT

/sbin/iptables -I INPUT -p tcp --dport 8080 -j ACCEPT

2）保存。

/etc/rc.d/init.d/iptables save

3）查看打开的端口。

/etc/init.d/iptables status

4）启动、关闭防火墙服务。

启动服务

service iptables start

关闭服务

service iptables stop

5）设置开机时启用、禁用防火墙服务。

启用服务

chkconfig iptables on

禁用服务

chkconfig iptables off

四、云平台访问策略配置
如果您购买的是云服务器，除了配置云服务器的防火墙，还需要登录云服务器提供商的管理平台配置访问策略（或安全组）。

不同云服务器提供商的管理平台操作方法不同，具体方法请查阅云服务器提供商的操作手册、或者百度，或者咨询云服务器提供商的客服。

# ftp
一、ftp简介
ftp（File Transfer Protocol文件传输协议）是基于TCP/IP 协议的应用层协议，用于文件的传输，包括ftp服务器（或服务端）和ftp客户端。

ftp客户端与服务器创建网络连接，请求登录服务器，登录成功后，就可以进行文件传输，主要包括下载文件和上传文件两种操作。

ftp协议很古老，有人说它技术太落后，不安全，对于这种说法我不于评论。但是，ftp的应用场景仍非常广泛，这是不争的事实。

在Linux系统中，ftp客户端和ftp服务器是操作系统自带的，但不一定会缺省安装。

二、安装ftp软件包
在CentOS7中，采用yum来安装ftp软件包，包括ftp服务器和ftp客户端。如果已经安装，再次执行yum就会把软件包升级到最新版本。

1、安装ftp服务器
yum -y install vsftpd

2、安装ftp客户端
yum -y install ftp 

三、配置ftp服务器
ftp的传输模式有被动模式和主动式两种，缺省是被动模式，主动模式的应用场景极少，为了方便表达，在接下来的内容中只介绍被动模式，主动模式在本文中也有介绍。

1、关闭SELINUX
修改/etc/selinux/config文件，把SELINUX参数的值改为disabled。

SELINUX =disabled

重启linux系统或执行 setenforce 0 使修改马上生效。

2、配置ftp数据端口参数
ftp的数据端口也称为高端口，在/etc/vsftpd/vsftpd.conf文件中配置，由pasv_min_port和pasv_max_port两个参数指定，如果文件中没有这两个参数，手工的加进去。

pasv_min_port=5000   # 高端口范围的最小值。

pasv_max_port=5500   # 高端口范围的最大值。

3、开通防火墙
开通防火墙的方法有两种：

1）开通ftp服务。

firewall-cmd --zone=public --add-service=ftp --permanent

2）开通ftp服务需要的端口，21是控制端口，5000-5500是数据端口范围，也就是上一节中在/etc/vsftpd/vsftpd.conf文件中配置的pasv_min_port和pasv_max_port参数。

firewall-cmd --zone=public --add-port=21/tcp --permanent

firewall-cmd --zone=public --add-port=5000-5500/tcp --permanent

重启防火墙：

systemctl restart firewalld.service

4、启动vsftpd服务
ftp服务器的服务名是vsftpd，相关的操作如下：

systemctl start    vsftpd   # 启动服务。

systemctl stop    vsftpd    # 停止服务。

systemctl restart vsftpd    # 重启服务。

systemctl status  vsftpd    # 查看服务状态。

systemctl enable  vsftpd    # 启用开机自动动vsftpd服务。

systemctl disable vsftpd    # 禁用开机自动动vsftpd服务。

5、云平台访问策略配置
如果您购买的是云服务器上，需要登录云服务器提供商的管理平台开通访问策略（或安全组），开通21和高端口的访问策略。

不同云服务器提供商的管理平台操作方法不同，具体操作方法阅读操作手册、或者百度，或者咨询云服务器提供商的客服。

如果云服务器的ftp服务不能建立数据会话，在百度中输入“被动模式下FTP不能建立数据会话问题“可以找到解决问题的方法，目前的阿里云服务器就存在这个问题。

四、主动模式和被动模式
ftp有两种模式，分别是port模式（主动模式）和pasv模式（被动模式）。

1、主动模式
客户端给服务端的21端口发命令说：我要输传文件，我已经打开了自己的20端口，您向我的20端口发起TCP连接，我们来传输文件。服务端知道后，就会主动向客户端的20端口发起连接，连接成功后开始传输文件。

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584496725331094693.png)

在主动模式下，ftp请求是由客户端TCP连接的；传输数据的时候，TCP连接却是由服务端发起的。

2、被动模式
客户端给服务器端的21端口发命令说：我要传输文件。服务器端知道后打开一个空闲的高端口，然后告诉客户端，我已经打开了某某端口，您向我这个端口发起TCP连接，然后我们用这个端口来传输文件。

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584496743101073294.png)

在被动模式下，不管是ftp命令，还是传输数据，都是由客户端向服务端发起TCP连接。

3、从主动模式到被动模式
在很久以前每台电脑都有一个ip地址，ftp只有主动模式，后来出现了共享上网技术，所以也就有了下面的问题。

共享上网就是多台电脑共享一个公网ip去使用internet，例如某个局域网出口的公网ip是210.33.25.108，当内网用户（192.168.1.100）访问外网的ftp服务器时，如果采用主动模式，192.168.1.100告诉了ftp服务器我需要某个文件和我打开了20端口之后，由于共享上网的原因，192.168.1.100在出网关的时候ip已经被转换成了210.33.25.108，所以ftp服务器端收到的消息是210.33.25.108需要某个文件并打开了20端口，ftp服务器就会尝试连接210.33.25.108的20端口，这样当然不会成功。

在主动模式中，ftp的两个端口是相对固定的，如果命令端口是n的话，那数据端口就是n-1，也就是说默认情况下，命令端口是21，数据端口就是20，如果您把ftp服务的端口改成了521，那么数据端口就是520，这样配置防火墙很方便，只需要开通两个端口就可以了。但是，在共享上网的环境中无法使用主动模式。

在被动模式中，默认情况下命令端口是21，数据端口是随机分配的。但是，被动模式中数据端口的范围可以配置，防火墙也可以配置端口范围。

# ftp命令
一、安装ftp客户端软件包
在CentOS7中，用root登录执行yum安装ftp客户端软件包，如果已经安装，再次执行yum就会把软件包升级到最新版本。

yum -y install ftp

二、ftp的用户
缺省情况下，ftp服务器操作系统用户名/密码也是ftp客户端登录的用户名/密码。root用户的权限过大，不允许登录ftp服务器。

三、登录服务器
方法一：输入ftp 服务器ip地址，回车后根据提示输入用户名和密码，如下图：
![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584497191447014107.png)

方法二：输入ftp，用open 服务器ip地址，连上服务器后再输入用户名和密码，如下图：

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584497204098039003.png)

方法三：输入ftp -n 服务器ip地址，再输入user 用户名 密码登录，如下图：
![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584497220142044175.png)

四、切换工作目录
注意，如果目录名中有特殊符号，如空格，可以用双引号把目录名包含起来。

1、查看服务器工作目录
pwd

2、切换服务器工作目录
cd 目录名

3、切换本地工作目录
lcd 目录名

五、查看服务器上的目录和文件
1、列出目录或文件名的详细信息
ls  目录或文件名

dir 目录或文件名

ls和dir都可以用于查看目录和文件信息，常用ls，语法和Linux的ls命令相同。

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584497254032051838.png)

2、仅列出目录和文件名
nlist 目录或文件名 [本地文件名]

1）列出/freecplus目录下的匹配*.h的文件名信息。

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584497267120018336.png)

2）列出/freecplus目录下的匹配*.h的文件名信息，结果输出到本地的/tmp/freecplus.list文件中。

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584497279752073683.png)

查看/tmp/freecplus.list内容。

![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584497291696001438.png)

六、下载/上传文件
1、文件传输入的模式
ftp的传输模式分为二进制和ASCII码两种模式，二进制模式可以传输任何文件，包括压缩包、可执行程序、图片、视频、音频等，而ASCII模式只能传输.txt、.htm等ascii码文件（文本文件）。在实际开发中，不管什么文件，都用二进制方式传输文件。

1）查看当前的传输模式。

type

2）设定传输模式为二进制。

bin

3）设定传输模式为ASCII。

ascii

示例：
![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584497308947074214.png)

2、下载文件
1）下载单个文件。

get|recv 服务器文件名 [本地文件名]

使用说明：

a）下载文件用get和recv都可以。

b）文件名不允许用通配符。

c）服务器文件名和本地文件名可以用绝对路径，如果不写路径，表示当前工作目录。

d）如果本地文件名省略不写，表示把服务器文件下载到本地的当前工作目录，文件名与服务器文件名相同。

2）下载多个文件。

mget 服务器文件1 服务器文件2 服务器文件3 …… 服务器文件n

使用说明：

a）待下载的文件名，可以一一列出来（用空格分隔），也可以用通配符。

b）下载的文件，存放在本地当前工作目录中。

c）下载文件时，会一一提示，如果想关闭都显示信息，先输入prompt命令。

prompt

3、上传文件
1）上传单个文件。

put|send 本地文件名 [服务器文件名]

a）上传文件用put和send都可以。

b）文件名不允许用通配符。

c）本地文件名和服务器文件名可以用绝对路径，如果不写路径，表示当前工作目录。

d）如果服务器文件名省略不写，表示把本地文件上传到服务器的当前工作目录，文件名与本地文件名相同。

2）上传多个文件。

mput 本地文件1 本地文件2 本地文件3 …… 本地文件n

使用说明：

a）待上传的文件名，可以一一列出来（用空格分隔），也可以用通配符。

b）上传的文件，存放在服务器当前工作目录中。

c）上传文件时，会一一提示，如果想关闭都显示信息，先输入prompt命令。

prompt

七、其它ftp命令
1）重命名服务器上的文件

rename 旧文件名 新文件名

2）删除ftp服务器上单个文件

delete 文件名

3）删除多个文件。

mdelete 文件名1 文件名2 文件名3 …… 文件名n

4）在服务器上创建目录。

mkdir pathname

5）删除服务器上的目录。

rmdir pathname

6）切换传输模式。

passive

7）显示帮助信息。

help [命令名]

显示ftp命令的帮助信息，如果不输入命令名，则显示全ftp命令的帮助信息。

8）退出ftp。

bye

八、Windows的ftp客户端
在Windows的DOS命令提示符下输入ftp命令，但是不好用。

打开资源管理器，输入：ftp://服务器ip地址，如下图：
![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584497391823007759.png)

在空白的位置点鼠标右键，选择登录菜单，如下图：
![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584497419078715366.png)

输入用户名和密码登录ftp服务器，如下图：
![](https://freecplus.net/runoobFiles/ueditor/image/20200318/1584497437005047170.png)

接下来的操作就像windows的目录文件操作一样了。