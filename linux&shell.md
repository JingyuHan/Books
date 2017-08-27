#第二章 走进shell#

　　在图形化界面出现前，与Unix系统进行交互的唯一方式是借助shell所提供的文本命令行界面（command line interface，CLI）。CLI只能接受文本输入，也只能显示出文本和基本的图形输出。<br>
　　在大多数linux发行版中，可以通过按下Ctrl+Alt组合键，然后按下功能键（F1~F7）来进入要使用的虚拟控制台。通常F1或F7是进入图形界面。Ubuntu是使用F7。

	setterm命令
	选项：
		-background		[black|red|green|yellow|blue|magenta|cyan|white]
						修改中断的背景色
		-foreground		[black|red|green|yellow|blue|magenta|cyan|white]
						修改终端的前景色
		-inversescreen 	[on|off]
						交换前景色和背景色
		-reset			none
						将终端外观恢复为默认设置并清屏
		-store			none
						将当前前景色和背景色设置为-reset选项的值

<br><br>
#第三章 bash手册#

##3.3 bash手册##

	man命令
		man <命令>
			查找命令手册，按空格翻页，按回车逐行查看，按q离开
		man  -k <命令关键词>
			按关键词查找命令

　　手册页将命令相关的信息分成不同的节，每一节惯用的命名标准如下：

	 节                                 描述
	------------------------------------------------------------
	Name                            显示命令名和一段简短的描述
	Synopsis                        命令的语法
	Configuration                   命令的配置信息
	Description                     命令的一般描述
	Options                         命令选项描述
	Exit Status                     命令的退出状态指示
	Return Value                    命令的返回值
	Error                           命令的错误信息
	Enviroment                      描述所使用的环境变量
	Files                           命令用到的文件
	Versions                        命令的版本信息
	Conforming To                   命令所遵从的标准
	Notes                           其他有帮助的资料
	Bugs                            提供提交bug的途径
	Example                         展示命令的用法
	Author                          命令开发人员信息
	Copyright                       命令源代码的版权状况
	See Also                        其他该命令类型的命令

　　还可以使用 info <命令> 及 <命令> -help 查看更多帮助信息。

##3.4浏览文件系统##

　　Linux将文件存储在单个目录结构中，这个目录结构称为虚拟目录（virtual directory）。虚拟目录将安装在PC上的所有存储设备的文件路径纳入耽搁目录结构中。
　　Linux虚拟目录结构只包含一个称为根（root）目录的基础目录。Linux中使用正斜线（/）在文件路径中划分目录。而反斜线（\）用来标识转义字符。
　　在Linux PC上安装的第一块硬盘称为根驱动器。根驱动器包含了虚拟目录的核心，其他目录都是从那里开始创建的。Linux会在根驱动器上创建一些特别的目录，称为挂载点（mount point）。挂载点是虚拟目录中用于分配额外存储设备的目录。虚拟目录会让文件和目录出现在这些挂载点目录中，然而实际上他们却存储在另外一个驱动器中。通常系统文件会存储在根驱动器中，而用户文件则存储在另一个驱动器中。

　　常见的Linux目录名称如下:

	 目录								用途
	------------------------------------------------------------------------
	/                               虚拟目录的根目录。通常不会在这里存储文件
	/bin                            二进制目录，存放很多用户级的GNU工具
	/boot                           启动目录，存放启动文件
	/dev                            设备目录，Linux在这里创建设备节点
	/etc                            系统配置文件目录
	/home                           主目录，Linux在这里创建用户目录
	/lib                            库目录，存放系统和应用程序的库文件
	/media                          媒体目录，可移动媒体设备的常用挂载点
	/mnt                            挂载目录，另一个可移动媒体设备的常用挂载点
	/opt							可选目录，常用于存放第三方软件包和数据文件
	/proc                           进程目录，存放现有硬件及当前进程的相关信息
	/root                           root用户的主目录
	/sbin                           系统二进制目录，存放许多GNU管理员级工具
	/run                            运行目录，存放系统运行时的运行时数据
	/srv                            服务目录，存放本地服务的相关文件
	/sys                            系统目录，存放系统硬件信息的相关文件
	/tmp                            临时目录，可以在该目录中创建和删除临时工作文件
	/usr                            用户二进制目录，大量用户级的GNU工具和数据文件都存储在这里
	/var                            可变目录，用来存放经常变化的文件，比如日志文件

　　切换目录命令:

	cd <destination>

　　显示当前所在目录：

	pwd

　　destination参数可以用两种方式表示：一种是绝对文件路径，另一种是使用相对文件目录。绝对文件路径总是以正斜线（/）作为开始，指明虚拟目录的根目录。可以清晰表明用户想切换到的确切位置。相对文件路径允许用户指定一个基于当前位置的目标文件路径。相对文件路径不以代表根目录的正斜线（/）开头，而是以目录名（如果用户准备切换到当前工作目录下的一个目录）或是一个特殊字符开始。有两个特殊字符可用于相对文件路径中：

	单点符（.），表示当前目录
	双点符（..），表示目前目录的父目录

##3.5 文件和目录列表##

　　列表命令（ls），ls命令输出的列表是按字母排序的（按列排序而不是按行排序）。若终端仿真器支持彩色，会用不同的颜色区分不同类型的文件。LS_COLORS控制这个功能。若不支持彩色，可用带-F参数的ls命令区分文件和目录。-F参数会在目录名后面加正斜线（/）来区分，在可执行文件后面加星号（*），在软链接文件后加'@'。

	ls -F

　　Linux常用隐藏文件来保存配置信息。隐藏文件通常是文件名以点号（.）开头的文件。这些文件不会在默认的ls命令输出中显示出来，若要显示这些隐藏文件，就需要-a参数。

	ls -a

　　-R参数会列出当前目录下包含的子目录下的文件，称为递归选项。

	ls -R

　　基本的ls命令不会输出太多每个文件的相关信息。要显示附加信息，常用的参数为-l。这种长列表格式的输出在每一行中列出了单个文件或文件。除了文件名，还包含一下信息：

- 文件类型，如目录（d），是directory的缩写；文件（-）；链接（l），是link的缩写；字符型文件（c），是character的缩写，该文件是一个字符设备文件，即一次传输一个字节的设备如键盘或字符型终端；块设备（b），是block的缩写，块设备是一次传输一整块数据的设备，如硬盘，光盘等，最小数据传输单位为一个数据块，通常为512字节；命令管道（p），sock（s）。
- 文件权限，三个一组，分别代表主权限，组权限和其他用户权限。-代表无权限，r代表具有可读权限，w代表具有可写权限，x代表具有可执行权限。
- 文件的硬链接总数。
- 文件属主的用户名。
- 文件属组的组名。
- 文件大小。
- 文件的上次修改时间。
- 文件名或目录名

　　ls命令支持在命令行中定义过滤器来决定显示哪些文件或目录。这个过滤器就是一个进行简单文本匹配的字符串。可在命令行参数之后添加过滤器。支持通配符。

- 问号（?），代表一个任意字符。
- 星号（*），代表零个或多个字符。
- 中括号及可能出现的字符，如[ai]表示a或者i，[a - i]表示从a到i的一个字符。
- 感叹号（!），排除一些字符。
- ……

##3.6 处理文件##

　　touch命令可以创建指定新文件，并将你的用户名作为文件属主。文件大小为零，因为touch值创建一个空文件。touch文件还可以用来改变文件的修改时间，这个操作并不改变文件的内容。若只想修改访问时间，可用-a参数。只是用ls -l命令，不会显示访问时间，若想查看访问时间，需要加入另一个参数：--time=atime。

	[root@localhost ~]# touch test
	[root@localhost ~]# ll test
	-rw-r--r--. 1 root root 520 8月  12 02:23 test
	[root@localhost ~]# touch test
	[root@localhost ~]# ll test
	-rw-r--r--. 1 root root 520 8月  12 02:24 test
	[root@localhost ~]# touch -a test
	[root@localhost ~]# ll test
	-rw-r--r--. 1 root root 520 8月  12 02:24 test
	[root@localhost ~]# ll --time=atime test
	-rw-r--r--. 1 root root 520 8月  12 02:25 test

　　cp命令可以在文件系统中，将文件和目录从一个位置复制到另一个位置。在基本的用法中，cp命令需要两个参数————源对象和目标对象：

	cp <source> <destination>

　　当source和destination参数都是文件名时，cp命令将源文件复制成一个新文件，并且destination命名。若destination为目录名，则将源文件复制到destination目录下，和源文件同名。新文件像全新文件一样，有新的修改时间。如果目标文件已经存在，cp命令会自动覆盖。加上-i参数，可以强制shell询问是否需要覆盖已有文件。

　　-R参数可以递归地复制整个目录的内容。

	cp -R <source> <destination>

　　支持通配符。
　　shell还有制表键自动补全功能。自动补全允许在输入文件名或目录名时按一下制表键，shell会将内容自动补充完整。使用制表键自动补全的技巧在于要给shell足够的文件名信息，使其能够将需要的文件与其他文件区分开。当无法完成自动补全时，会听到‘嘟’的一声。要是再按一下制表键，shell就会列出所有匹配的文件名。
　　链接文件是linux文件系统的一个优势。若需要在系统上维护同一个文件的两份或多份备份，除了保存多份单独的物理文件备份外，还可以采用保存一份物理文件副本和多个虚拟副本的方法。这种虚拟的副本就称为链接。链接是目录中指向文件真实位置的占位符。在Linux中有两种不同类型的文件链接：

- 符号链接
- 硬链接

　　符号链接就是一个实实在在的文件，它指向放在虚拟目录结构中某个地方的另一个文件。这两个通过符号链接在一起的文件，彼此的内容并不相同。要为一个文件创建符号链接，原始文件必须事先存在。然后可以使用ln命令以及-s选项来创建符号链接。类似windows下的快捷方式。

	[root@localhost ~]# ll test*
	-rw-r--r--. 1 root root 520 8月  12 02:20 test
	[root@localhost ~]# ln -s test test_sl
	[root@localhost ~]# ll test*
	-rw-r--r--. 1 root root 520 8月  12 02:20 test
	lrwxrwxrwx. 1 root root   4 8月  12 02:21 test_sl -> test
	[root@localhost ~]# ll -i test*
	529974 -rw-r--r--. 1 root root 520 8月  12 02:24 test
	529745 lrwxrwxrwx. 1 root root   4 8月  12 02:21 test_sl -> test
	[root@localhost ~]#

　　符号链接文件与源文件是两个完全不同的文件，由上例可以看到，源文件为520字节，而符号链接文件只有4字节，并且inode编号也不一样。
　　硬链接会创建独立的虚拟文件，其中包含了原始文件的信息及位置。他们从根本上来说是同一个文件。引用硬链接文件等同于引用了源文件。要创建硬链接，原始文件必须事先存在，只不过这次使用的ln命令时不需要加入额外的参数了。

	[root@localhost ~]# ll test*
	-rw-r--r--. 1 root root 520 8月  12 02:20 test
	[root@localhost ~]# ln test test_hl
	[root@localhost ~]# ll -i test*
	529974 -rw-r--r--. 2 root root 520 8月  12 02:24 test
	529974 -rw-r--r--. 2 root root 520 8月  12 02:24 test_hl

　　带有硬链接的文件共享inode编号，文件大小也一模一样。它们终归是同一个文件。注意：只能对处于同一存储媒体的文件创建硬链接，要想在不同存储媒体的文件之间创建链接，只能使用符号链接。
　　复制链接文件时一定要小心。当复制一个已经被链接到另一个源文件的文件时，得到的是源文件的副本。不需要复制链接文件，可以创建原始文件的另一个链接。千万不要创建软链接文件的软链接，这样会形成混乱的链接链，不仅容易断裂，还会造成各种麻烦。
　　mv命令可以将文件或目录移动到另一个位置或重命名。文件的时间戳和inode编号都不变，改变的只有位置和名称。

	mv <source> <destination>

　　rm命令可以移除文件（removing）。文件一旦移除，就无法找回。在试用rm命令时，习惯加入-i参数。加入-f参数可以不受提示符打扰，强制移除。

	rm -i <file>

##3.7 处理目录##

　　mkdir命令可以创建新目录。

	mkdir <directory>

　　想要同时创建多个目录和子目录，需要加入-p参数，它会根据需要创建缺失的父目录。

	[root@localhost ~]# mkdir testff/testf/test
	mkdir: 无法创建目录"test/test/test": 没有那个文件或目录
	[root@localhost ~]# mkdir -p testff/testf/test
	[root@localhost ~]# ls -R testff
	testff:
	testf

	testff/testf:
	test

	testff/testf/test:
	[root@localhost ~]#

　　移除目录的基本命令rmdir，但它只能删除空目录。rmdir没有-i参数来询问是否移除目录。可以使用rm命令加-r参数（对于rm命令，-r和-R参数的效果是一样的），他会向下进入目录，移除其中的文件，然后移除目录本身。

	[root@localhost ~]# rmdir testff
	rmdir: 删除 "testff" 失败: 目录非空
	[root@localhost ~]# rm -ri testff
	rm：是否进入目录"testff"? y
	rm：是否进入目录"testff/testf"? y
	rm：是否进入目录"testff/testf/test"? y
	rm：是否删除普通空文件 "testff/testf/test/testfile"？y
	rm：是否删除目录 "testff/testf/test"？y
	rm：是否删除目录 "testff/testf"？y
	rm：是否删除目录 "testff"？y
	[root@localhost ~]#

　　这样需要确认每个文件或目录是否要移除，可以加-f参数忽略询问强制移除。

	[root@localhost ~]# rm -rif testff
	[root@localhost ~]# ls testff
	ls: 无法访问testff: 没有那个文件或目录
	[root@localhost ~]#

　　使用tree工具可以直观的展示目录、子目录及其中的文件。

##3.8 查看文件内容##

　　file命令可以探测文件内部，并决定文件是什么类型。如果是文本文件，还能确定编码方式。如果是链接文件，能够确定他链接在哪个文件上。如果是一个二进制可执行程序，能够确定该程序编译时所面向的平台以及所需类库。

	file <filename>

　　cat命令可以显示文本文件中的所有数据。-n参数可以给所有的行加上行号，-b参数可以只给有文本的行加上行号，-T参数可以将制表符替换为^I。

	[root@localhost ~]# cat test
	This is a test file

		This is a test file

	This is a test file
	[root@localhost ~]# cat -n test
	     1	This is a test file
	     2	
	     3		This is a test file
	     4	
	     5	This is a test file
	[root@localhost ~]# cat -b test
	     1	This is a test file
	
	     2		This is a test file
	
	     3	This is a test file
	[root@localhost ~]# cat -T test
	This is a test file

	^IThis is a test file

	This is a test file
	[root@localhost ~]# 

　　cat命令的缺陷是，一旦运行，就无法控制后面的操作，文本会在显示器上一晃而过。
　　more命令则会在显示每页数据之后停下来，在屏幕底部，more命令会显示一个标签，来标明仍然在more程序中以及在文本文件中的位置。和手册页中一样，可以通过空格键换行，回车键逐行前进的方式浏览文本，按q退出。

	more <filename>

　　less命令是more命令的升级版，它提供了一些实用的特性，能够在文本文件中前后翻动，而且还有一些高级搜索的功能。它能够识别方向键以及翻页键。

	less <filename>

　　tail命令会显示文本最后几行的内容，默认情况下显示末尾10行。可以在tail命令中加入参数-n来修改显示的行数。-f参数允许你在其他进程使用该文件时查看文件的内容。tail命令会保持活动状态，并不断显示添加到文件中的内容。这是实时监测系统日志文件的绝妙方式。

	tail [option] <filename>
		-n 修改显示行数
		-f 实时显示

　　head命令与tail命令类似，不过它是显示文件开头的几行内容，默认情况下显示开头10行。也支持-n参数。

	head [option] <filename>
		-n 修改显示行数

#第四章 更多的bash shell命令#

##4.1 监测程序##

　　当程序运行在系统上时，我们称之为进程（process）。ps命令可以监测这些进程。默认情况下，ps命令只会显示运行在当前控制台下的属于当前用户的进程。

	ps

　　linux系统中使用的GNU ps命令支持3种不同类型的命令行参数：
- Unix风格的参数，前面加单破折线
- BSD风格的参数，前面不加破折线
- GNU风格的长参数，前面加双破折线

###Unix风格参数###

	 参数                        描述
	-A                        显示所有进程
	-N                        显示与指定参数不符的进程
	-a                        显示除控制进程（session leader）和无终端进程外的所有进程
	-d                        显示除控制台进程外的所有进程
	-e                        显示所有进程
	-C cmdlist                显示包含在cmdlist列表中的进程
	-G grplist                显示组ID在grplist列表中的进程
	-U userlist               显示属主的用户ID在userlist中的进程
	-g grplist                显示会话或组ID在grplist列表中的进程
	-p pidlist                显示PID在pidlist列表中的进程
	-s sesslist               显示会话ID在sesslist列表中的进程
	-t ttylist                显示终端ID在ttylist列表中的进程
	-u userlist               显示有效用户ID在userlist列表中的进程
	-F                        显示更多额外输出（相对-f参数而言）
	-O format                 显示默认的输出列以及format列表指定的特定列
	-M                        显示进程的安全信息
	-c                        显示进程的额外调度器信息
	-f                        显示完整格式的输出
	-j                        显示任务信息
	-l                        显示长列表
	-o format                 仅显示有format指定的列
	-y                        不要显示进程标记（process flag，表明进程状态的标记）
	-Z                        显示安全标签（security context）信息
	-H                        用层级格式来显示进程（树状，用来显示父进程）
	-n namelist               定义了WCHAN列显示的值
	-w                        采用宽输出模式，不限宽度显示
	-L                        显示进程中的线程
	-V                        显示ps命令的版本号

　　一般可以使用ps -ef命令来查看系统上运行的所有进程，其中：

- UID：启动这些进程的用户
- PID：进程的进程ID
- PPID：父进程的进程号（如果该进程是由另一个进程启动的）
- C：进程生命周期中的CPU利用率
- STIME：进程启动时的系统时间
- TTY：进程启动时的终端设备
- TIME：运行进程需要的累积CPU时间
- CMD：启动的程序名称

　　如果想获得更多的信息，可以采用-l参数，它会产生一个长格式的输出，会多出以下列：

- F：内核分配给进程的系统标记
- S：进程的状态（O代表正在运行；S代表在休眠；R表示可运行，正等待运行；Z表示僵化，进程已经结束但父进程已不存在；T表示停止）
- PRI：进程的优先级（越大的数字代表越低的优先级）
- NI：谦让度值，用来参与决定优先级
- ADDR：进程的内存地址
- SZ：假如进程被换出，所需交换空间的大小
- WCHAN：进程休眠的内核函数的地址

###BSD风格的参数###

	 参数                        描述
	T                         显示跟当前终端关联的所有进程
	a                         显示跟任意中断关联的所有进程
	g                         显示所有进程，包括控制进程
	r                         仅显示运行中的进程
	x                         显示所有的进程，包括未分配任何终端的进程
	U userlist                显示归userlist列表中某用户ID所有的进程
	p pidlist                 显示PID在pidlist列表中的进程
	t ttylist                 显示所关联的终端在ttylist列表中的进程
	O format                  除了默认输出的列之外，还输出由format指定的列
	X                         按过去的Linux i386寄存器格式输出
	Z                         将安全信息添加在输出中
	j                         显示任务信息
	l                         采用长模式
	o format                  仅显示由format指定的列
	s                         采用信号格式显示
	u                         采用基于用户的格式显示
	v                         采用虚拟内存格式显示
	N namelist                定义在WCHAN列中使用的值
	O order                   定义显示信息列的顺序
	S                         将数值信息从子进程加到父进程中，比如CPU和内存的使用情况
	c                         显示真实的命令名称（用以启动进程的进程名称）
	e                         显示命令使用的环境变量
	f                         用分层格式来显示进程，表明哪些进程启动了哪些进程
	h                         不显示头信息
	k sort                    指定用以将输出排序的列
	n                         和WCHAN信息一起显示出来，用数值来表示用户ID和组ID
	w                         为较宽屏幕显示宽输出
	H                         将线程按进程来显示
	m                         在进程后显示线程
	L                         列出所有格式指定符
	V                         显示ps命令的版本号

　　大部分输出跟使用Unix风格参数时的输出是一样的，只有一小部分不同。

- VSZ：进程在内存中的大小，以千字节（KB）为单位
- RSS：进程在未换出是占用的物理内存
- STAT：代表当前进程状态的双字符状态码

　　这里的进程状态码（STAT列）使用双字符状态码，比Unix风格输出的单字符状态码更清楚地展示进程的当前状态。第一个字符采用了和Unix风格S列相同的值，表明进程是在休眠、运行还是等待。第二个参数进一步说明进程的状态：

- <：该进程运行在高优先级上
- N：该进程运行在低优先级上
- L：该进程有页面锁定在内存中
- s：该进程是控制进程
- l：该进程是多线程的
- +：该进程运行在前台

###GNU长参数###

	 参数                        描述
	--deselect                显示所有进程，命令行中列出的进程
	--Group grplist           显示组ID在grplist列表中的进程
	--User userlist           显示用户ID在userlist列表中的进程
	--group grplist           显示有效组ID在grplist列表中的进程
	--pid pidlist             显示PID在pidlist列表中的进程
	--sid sidlist             显示会话ID在sidlist列表中的进程
	--tty ttylist             显示终端设备号在ttylist列表中的进程
	--user userlist           显示有效用户ID在userlist列表中的进程
	--format format           仅显示由format指定的列
	--context                 显示额外的安全信息
	--cols n                  将屏幕宽度设置为n列
	--columns n               将屏幕宽度设置为n列
	--cumulative              包含已停止的子进程的信息
	--forest                  用层级结构显示出进程和父进程之间的关系
	--headers                 在每页输出中都显示列的头
	--no-headers              不显示列的头
	--lines n                 将屏幕高度设置为n行
	--rows n                  将屏幕高度设置为n行
	--sort order              指定将输出按哪列排序
	--width n                 将屏幕宽度设置为n列
	--help                    显示帮助信息
	--info                    显示调试信息
	--version                 显示ps命令的版本号


　　ps命令可以收集运行在系统上的进程信息，但只能显示某个特定时间点的信息。无法用来观察那些频繁换进换出内存的进程趋势。
　　top命令能够实时地显示进程信息。

	top

　　top命令输出的第一部分显示的是系统的概况：
　　第一行显示了当前时间，系统的运行时间，登录的用户数以及系统的平均负载。平均负载有3个值：最近1分钟，最近5分钟和最近15分钟的平均负载。值越大说明系统的负载越高。由于进程短期的突发性活动，出现最近1分钟的高负载值也很常见，但如果近15分钟内的平均负载都很高，就说明系统可能有问题。Linux系统的高负载值取决于系统的硬件配置以及系统上通常运行的程序。对某个系统来说的高负载的值可能对另一个系统来说就是正常值。通常，若系统的负载值超过了2，就说明系统比较繁忙了。
　　第二行显示了进程概要信息————top命令的输出中将进程叫做任务（task）：有多少进程处在运行、休眠、停止或是僵化状态（僵化状态是指进程完成了，但父进程没有响应）。
　　第三行显示了CPU的概要信息。显示的内容为“Cpu(s):  0.0%us,  0.1%sy,  0.0%ni,100.0%id,  0.0%wa,  0.0%hi,  0.0%si,  0.0%st”，分别对应：用户空间占用CPU百分比、内核空间占用CPU百分比、用户空间内改变过优先级的进程占用CPU百分比、空闲CPU百分比、等待输入输出CPU时间百分比、CPU服务于硬件中断所耗费的时间总额、CPU服务软中断所耗费的时间总额、Steal Time。
　　下两行显示了系统内存的状态。第一行显示系统的物理内存：“Mem:   1030608k total,   151024k used,   879584k free,    15596k buffers”，分别对应：物理内存总量、已使用的物理内存、空闲物理内存、内核缓存内存量。后一行说的是同样的信息，不过是针对系统交换空间（如果分配了的话）的状态而言的。
　　最后一部分显示了当前运行中的进程的详细列表，有些列跟ps命令的输出类似。

- PID：进程的ID
- USER：进程属主的名字
- PR：进程的优先级
- NI：进程的谦让度值
- VIRT：进程占用的虚拟内存总量
- RES：进程占用的物理内存总量
- SHR：进程和其他进程共享的内存总量
- S：进程的状态（D代表可中断的休眠状态，R代表在运行状态，S代表休眠状态，T代表跟踪状态或停止状态，Z代表僵化状态）
- %CPU：进程使用的CPU时间比例
- %MEM：进程使用的内存占可用内存的比例
- TIME+：子进程启动到目前为止的CPU时间总量
- COMMAND：进程所对应的命令行名称，也就是启动的程序名

　　top命令运行时可以使用交互式命令改变top命令的行为。每个交互式命令都时单字符。

- 1：监控每个逻辑CPU的状况
- b：打开/关闭加亮效果
- c：切换显示命令名称或完整命令行
- f：添加或删除显示列
- h：显示帮助画面
- i：忽略/显示闲置和僵尸进程
- k：终止一个程序
- o：改变显示项目的顺序
- q：退出top命令
- s/d：改变两次刷新之间的延迟时间。输入0值则系统将不断刷新，该终端将会繁忙。
- S：切换到累计模式
- <：向左改变排序列
- \>：向右改变排序列
- x：打开/关闭排序列的加亮效果
- y：打开/关闭运行状态进程的加亮效果

　　在Linux中，进程之间通过信号来通信。Linux的信号包括：

- 1：HUP（挂起）
- 2：INT（中断）
- 3：QUIT（结束运行）
- 9：KILL（无条件终止）
- 11：SEGV（段错误）
- 15：TERM（尽可能终止）
- 17：STOP（无条件停止运行，但不终止）
- 18：TSTP（停止或暂停，但继续在后台运行）
- 19：CONT（在STOP或TSTP之后恢复执行）

　　在Linux中，有两个命令可以向运行中的进程发出进程信号。
　　kill命令可通过进程ID（PID）给进程发信号。

	kill

　　默认情况下，kill命令会向命令行中列出的全部PID发送一个TERM信号。要发送进程信号，必须是进程的属主或登录为root用户。
　　TERM信号告诉程序尽可能停止运行，但是有些程序可能会忽略这个请求。想要强制终止，-s参数支持指定其他信号，例如：

	[root@localhost ~]# kill -s HUP 3940
	[root@localhost ~]#

　　kill命令不会有任何输出。要检查kill命令是否有效，需要运行ps或top命令查看。
　　killall命令支持通过进程名来结束进程，支持通配符。以root用户身份登录时，要谨慎使用killall命令，可能会因误用通配符结束重要的系统进程，这可能会破坏文件系统。

	killall

##4.2 监测磁盘空间##

　　在今天的图形化桌面环境中，大多数Linux发行版都能自动挂载特定类型的可移动存储体。可移动存储媒体指的是可从PC上轻易移除的媒体，比如CD-ROM、软盘和U盘。如果用的发行版不支持自动挂载和卸载可移动存储媒体，就必须手动完成。
　　mount命令可以用来挂载媒体。默认情况下，mount命令会输出当前系统上挂载的设备列表。提供的信息包括：

- 媒体的设备文件名
- 媒体挂载到虚拟目录的挂载点
- 文件系统类型
- 已挂载媒体的访问状态

　　要手动在虚拟目录挂载设备，需要一root用户身份登录，或是以root用户身份运行sudo命令。手动挂载媒体设备的基本命令是：

	mount -t type device directory

　　type参数指定了磁盘 被格式化的文件系统类型。Linux可以识别非常的的文件系统类型，与Windows PC公用存储设备，通常会使用到下列文件系统类型：

- vfat：Windows长文件系统
- ntfs：Windows NT、XP、Vista以及Windows7中广泛使用的高级文件系统
- iso9660：标准CD-ROM文件系统

　　大部分U盘会被格式化为vfat文件系统，而数据CD必须使用ios9660文件系统类型。后两个参数定义了该存储设备的设备文件的位置以及挂载点在虚拟目录中的位置，比如手动将U盘/dev/sdb1挂载到/media/disk。可以用下面的命令：

	mount -t vfat /dev/sdb1 /media/disk

　　媒体设备挂在到了虚拟目录后，root用户就有了对该设备的所有访问权限，而其他用户的访问权限则会被限制。你可以通过目录权限指定用户对设备的访问权限。
　　mount命令的参数：

	 参数                        描述
	-a                        挂载/etc/fstab文件中指定的所有文件系统
	-f                        使mount命令模拟挂载设备，但并不是真的挂载
	-F                        和-a参数一起使用时，会同时挂载所有文件系统
	-v                        详细模式，将会说明挂载设备的每一步
	-I                        不启用任何/sbin/mount.filesystem下的文件系统帮助文件
	-l                        给ext2、ext3或XFS文件系统自动添加文件系统标签
	-n                        挂载设备，但不注册到/etc/mtab已挂载设备文件中
	-p num                    进行加密挂载时，从文件描述符num中获得密码短语
	-s                        忽略文件系统不支持的挂在选项
	-r                        将设备挂载为只读的
	-w                        将设备挂载为可读写的（默认参数）
	-L label                  将设备按指定的label挂载
	-U uuid                   将设备按指定的uuid挂载
	-O                        和-a参数一起使用，限制命令只作用到特定的一组文件系统上
	-o                        给文件系统添加特定的选项

　　-o参数允许在挂载文件系统时添加一些以逗号分隔的额外选项：

- ro：以只读形式挂载
- rw：以读写形式挂载
- user：允许普通用户挂载文件系统
- check=none：挂载文件系统时不进行完整性校验
- loop：挂载一个文件

　　从Linux系统上移除一个可移动设备时，不能直接从系统上移除，而应该先卸载。
　　umount命令用来卸载设备。命令格式为：

	umount [directory | device]

　　umount命令支持通过设备文件或者是挂载点来指定要卸载的设备。如果有任何程序正在使用设备上的文件，系统会不允许卸载。必要时可以用lsof命令获得使用它的进程，然后在应用中停止使用该设备或停止该进程。
　　df命令用来查看已挂载磁盘的使用情况。

	df

　　输出项有：

- 设备的设备文件位置
- 能容纳多少个1024字节大小的块
- 已用了多少个1024字节大小的块
- 还有多少个1024字节大小的块
- 已用空间所占的比例
- 设备挂载到了哪个挂载点上

　　-h参数可以把输出中的磁盘空间按易读的方式显示，单位转换为M或G。
　　du命令可以显示特定目录（默认情况下是当前目录）的磁盘使用情况。可以用来快速判断某个目录下是否有超大文件。

	du

　　默认情况下，du命令会显示当前目录下所有的文件、目录和子目录的磁盘使用情况，它会以磁盘块为单位来表明每个文件或目录占用了多大存储空间。对标准大小的目录来说，这个列表会很长。这个列表是从目录层级的最底层开始，然后按文件、子目录、目录逐级向上。
　　下面几个参数可以让du命令使用更加方便：

- -c：显示所有已列出文件总的大小
- -h：按用户易读的格式输出大小，即用K替代千字节，M替代兆字节，G替代吉字节。
- -s：显示该目录占用空间总和

##4.3 处理数据文件##

　　sort命令会按照会话指定的默认语言的排序规则对文本文件中的数据进行排序。
　　sort命令参数：

	单破折号        双破折号                    描述
	  -b       --ignore-leading-blanks    排序时忽略起始的空白
	  -C       --check=quiet              不排序，若数据无序不报告不输出
	  -c       --check                    不排序，检查是否已排序，若无序，报告
	  -d       --dictionary-order         仅考虑空白和字母，不考了特殊字符
	  -f       --ignore-case              忽略大小写
	  -g       --general-number-sort      按通用数值排序，转为浮点数排序，支持科学计数法
	  -i       --ignore-nonprinting       在排序时忽略不可打印字符
	  -k       --key=POS1[,POS2]          排序从POS1位置开始，若指定POS2，则到POS2位置结束
	  -M       --month-sort               用三字符月份名按月份排序
	  -m       --merge                    将两个已排序数据文件合并
	  -n       --numeric-sort             按字符串数值排序，不转换为浮点数
	  -o       --output=file              将排序结果写出到指定文件
	  -R       --random-sort              按随机生成的散列表的键值排序
	           --random-source=FILE       指定-R参数用到的随机字节的源文件
	  -r       --reverse                  反向排序
	  -S       --buffer-size=SIZE         指定使用的内存大小
	  -s       --stable                   禁用最后重排序比较
	  -T       --temporary-directory=DIR  指定一个位置来存储临时工作文件
	  -t       --field-separator=SEP      指定一个用来区分键位置的字符
	  -u       --unique                   重复行只显示一次，和-c参数一起使用时，输出第一例重复的两行

　　关于-k参数的探索：

	[root@localhost ~]# cat test
	1 25 3
	2 31 1
	2 28 2
	3 13 2
	1 12 1
	2 25 2
	[root@localhost ~]# sort test
	1 12 1
	1 25 3
	2 25 2
	2 28 2
	2 31 1
	3 13 2
	[root@localhost ~]# sort -k2 test                         #排序区域为从第二块第一个字符到结束
	1 12 1
	3 13 2
	2 25 2
	1 25 3
	2 28 2
	2 31 1
	[root@localhost ~]# sort -t ' ' -k 2.2 test               #排序区域为从第二块第二个字符到结束
	2 31 1
	1 12 1
	3 13 2
	2 25 2
	1 25 3
	2 28 2
	[root@localhost ~]# sort  -t ' ' -k 2.2,2.2 test          #排序区域仅为第二块第二个字符
	2 31 1
	1 12 1
	3 13 2
	1 25 3
	2 25 2
	2 28 2

　　grep命令会在输入或特定的文件查找包含匹配指定模式的字符的行并输出。命令格式如下：

	grep [options] pattern [file]

　　-v参数可以进行反向搜索即输出不匹配该模式的行；-n参数可以显示匹配模式的行所在行号；-c参数只输出有多少行匹配该模式；-e参数可以指定多个匹配模式，如：

	grep -e pattern1 -e pattern2 [file]

　　默认情况下，grep命令用基本的Unix风格正则表达式来匹配模式。
　　egrep命令是grep命令的衍生，支持POSIX扩展正则表达式。fgrep命令则是另一个版本，支持将匹配模式指定为用换行符分隔的一列固定长度的字符串。
　　Linux系统包含了多种文件压缩工具：

	 工具        文件扩展名                描述
	bzip2          .bz2               采用Burrows-Wheeler块排序文本压缩算法和霍夫曼编码
	compress       .Z                 最初的Unix文件压缩工具，已经快没人用了
	gzip           .gz                GNU压缩工具，用Lempel-Ziv编码
	zip            .zip               Windows上PKZIP工具的Unix实现

　　gzip命令是Linux上最流行的压缩工具。gzip软件包是GNU项目的产物。这个软件包包含以下工具：

- gzip：用来压缩文件
- zcat：用来查看压缩过的文本文件内容
- gunzip：用来解压文件

　　gzip命令支持通配符。
　　目前，Unix和Linux上最广泛使用的归档工具是tar命令。
　　tar命令最开始是用来将文件写到携带设备上归档的，然而它也能把输出写到文件中，这种用法在Linux上已经普遍用来归档数据了。tar命令格式为：

	tar function [options] object1 object2 ...

　　tar命令的功能有：

	 功能        长名称                描述
	-A        --concatenate       将一个已存在的tar归档文件追加到另一个已存在的tar归档文件
	-c        --create            创建一个新的tar归档文件
	-d        --diff              检查归档文件和文件系统的不同之处
              --delete            从已存在的tar归档文件中删除
	-r        --append            追加文件到已存在的tar归档文件末尾
	-t        --list              列出已存在tar归档文件的内容
	-u        --update            更新tar归档文件中已有的同名文件
	-x        --extract           从已有tar归档文件中提取文件

　　每个功能可用选项来针对tar归档文件定义一个特定行为。能与rar命令一起使用的常见选项有：

	 选项                             描述
	-C dir                        切换到指定目录
	-f dir                        输出结果到文件或设备file
	-j                            将输出重定向给bzip2命令来压缩内容
	-p                            保留所有文件权限
	-v                            在处理文件时显示文件
	-z                            将输出重定向给gzip命令来压缩内容

　　gzip命令压缩过的tar文件可以用命令tar -zxvf filename.tgz来解压。

#第五章 理解shell#

##5.1 shell的类型##

　　系统启动什么样的shell程序取决于个人的用户ID配置。在/etc/passwd文件中，在用户ID记录的第7个字段中列出了默认的shell程序。只要用户登录到某个虚拟控制台终端或是在GUI中启动终端仿真器，默认的shell程序就会开始运行。

	[root@localhost ~]# cat /etc/passwd
	root:x:0:0:root:/root:/bin/bash
	[...]
	[root@localhost ~]#

　　此例中，默认的shell程序是GNU bash shell。bash shell程序位于bin目录内，从长列表中可以看出/bin/bash是一个可执行文件：

	[root@localhost ~]# ll -F /bin/bash
	-rwxr-xr-x. 1 root root 874248 5月  11 2012 /bin/bash*
	[root@localhost ~]#

　　除此之外，还有源自最初的C shell的tcsh，还有ash shell的Debian版本dash等。还有一个默认shell是/bin/sh，他作为默认的系统shell，用于那些需要在启动时使用的系统shell脚本。

	[root@localhost ~]# ll /bin/sh
	lrwxrwxrwx. 1 root root 4 3月  19 2016 /bin/sh -> bash
	[root@localhost ~]#

　　此例中，系统默认的shell被设置为bash。
　　可以直接输入对应文件名来使用其他发行版中可用的shell，如：

	[root@localhost ~]# /bin/dash
	#
	# exit
	[root@localhost ~]# 

##5.2 shell的父子关系##

　　在CLI提示符后输入/bin/bash命令或其他等效bash命令时，会创建一个新的shell程序，这个shell程序被称为子shell（child shell）。bash shell是一个程序，当它运行时，就成为了一个进程，一个运行着的shell就是某个进程。在生成子shell时，只有部分父进程的环境被复制到子shell环境中。

	[root@localhost ~]# ps -f
	UID        PID  PPID  C STIME TTY          TIME CMD
	root      2155  2150  0 19:56 pts/0    00:00:00 -bash
	root      2524  2155  0 20:41 pts/0    00:00:00 ps -f
	[root@localhost ~]# bash
	[root@localhost ~]# bash
	[root@localhost ~]# bash
	[root@localhost ~]# ps -f --forest
	UID        PID  PPID  C STIME TTY          TIME CMD
	root      2155  2150  0 19:56 pts/0    00:00:00 -bash
	root      2565  2155  0 20:47 pts/0    00:00:00  \_ bash
	root      2574  2565  0 20:47 pts/0    00:00:00      \_ bash
	root      2583  2574  0 20:47 pts/0    00:00:00          \_ bash
	root      2593  2583  0 20:47 pts/0    00:00:00              \_ ps -f --forest
	[root@localhost ~]# exit
	exit
	[root@localhost ~]# ps -f --forest
	UID        PID  PPID  C STIME TTY          TIME CMD
	root      2155  2150  0 19:56 pts/0    00:00:00 -bash
	root      2565  2155  0 20:47 pts/0    00:00:00  \_ bash
	root      2574  2565  0 20:47 pts/0    00:00:00      \_ bash
	root      2596  2574  0 20:48 pts/0    00:00:00          \_ ps -f --forest
	[root@localhost ~]# exit
	exit
	[root@localhost ~]# exit
	exit
	[root@localhost ~]# ps -f --forest
	UID        PID  PPID  C STIME TTY          TIME CMD
	root      2155  2150  0 19:56 pts/0    00:00:00 -bash
	root      2597  2155  1 20:48 pts/0    00:00:00  \_ ps -f --forest
	[root@localhost ~]# 


　　此例中，可以看到创建了三个子shell，ps --forest命令展示了这些子shell间的嵌套结构。通过PID和PPID可以看出他们的父子关系。
　　exit命令不仅可以退出子shell，还能用来登出当前的虚拟控制台终端或终端仿真软件。只需在父shell中输入exit，就能退出CLI了。
　　只需在命令之间加入分号（；）就可以实现命令列表。而当这些命令包含在括号中时，就实现了进程列表。进程列表会生成一个子shell来执行对应的命令。借助环境变量的命令echo $BASH_SUBSHELL来查看是否生成了子shell。

	[root@localhost home]# pwd; cd /etc; pwd; cd /home; pwd; echo $BASH_SUBSHELL
	/home
	/etc
	/home
	0
	[root@localhost home]# (pwd; cd /etc; pwd; cd /home; pwd; echo $BASH_SUBSHELL)
	/home
	/etc
	/home
	1
	[root@localhost home]# (pwd; cd /etc; pwd; cd /home; pwd); echo $BASH_SUBSHELL
	/home
	/etc
	/home
	0
	[root@localhost home]# (pwd; cd /etc; pwd; cd /home; pwd; (echo $BASH_SUBSHELL))
	/home
	/etc
	/home
	2
	[root@localhost home]# 

　　可以看出每出现一对括号，就会生成一个子shell，而括号结束后，进程结束。
　　在交互式的CLI shell会话中，子shell并非真正的多进程处理，因为终端控制着子shell的I/O，所以采用子shell会明显拖慢处理速度。
　　在交互式shell中，一个高效的子shell用法是使用后台模式。在后台模式中运行命令可以在处理命令的同时让出CLI，以供他用。要想将命令置入后天模式，可以在命令行末尾加上字符＆。

	[root@localhost ~]# sleep 3000 &
	[1] 2166
	[root@localhost ~]# ps -f
	UID        PID  PPID  C STIME TTY          TIME CMD
	root      2145  2140  0 10:30 pts/0    00:00:00 -bash
	root      2166  2145  0 10:31 pts/0    00:00:00 sleep 3000
	root      2168  2145  0 10:31 pts/0    00:00:00 ps -f
	[root@localhost ~]# 

　　此例中，sleep命令会在后台（&）睡眠3000秒。当它被置入后台，shell CLI提示符返回之前会出现两天信息。第一条信息是显示在方括号中的后台作业（background job）号（1）。第二条是后台作业的进程ID（2166）。
　　除了ps命令，jobs命令可以显示出当前运行在后台模式中的所有用户的进程（作业）。

	[root@localhost ~]# jobs
	[1]+  Running                 sleep 3000 &
	[root@localhost ~]# 

　　jobs命令再方括号中显示出作业号（1），当前状态（running）以及对应的命令（sleep 3000 &）。
　　在CLI中运用子shell的创造性方法之一就是将进程列表置入后台模式。既可以在子shell中进行繁忙的处理工作，同时也不会让子shell的I/O受制于终端。
　　协程也是子shell在CLI中的创造性用法。协程可以同时做两件事。它在后台生成一个子shell，并在这个子shell中执行命令。要进行协程处理，需要使用coproc命令，还有要在子shell中执行的命令。

	[root@localhost ~]# jobs
	[1]+   Running                 coproc COPROC sleep 10 &
	[root@localhost ~]# 

　　可以看出在子shell中执行的后台命令是coproc COPROC sleep 10 &,COPROC是coproc命令给进程起的名字。可以使用扩展语法自定义进程名字。

	[root@localhost ~]# coproc My_Job { sleep 10; }
	[1] 2313
	[root@localhost ~]# jobs
	[1]+  Running                 coproc My_Job { sleep 10; } &
	[root@localhost ~]# 

　　使用扩展语法自定义进程名字时，需要确保花括号两边有空格。

##5.2 理解shell的內建命令##

　　shell命令分为內建命令和非內建（外部）命令。
　　外部命令，有时称为文件系统命令，是存在于bash shell之外的程序。外部命令程序通常位于/bin、/usr/bin、/sbin或/usr/sbin中。
　　利用which和type命令可以找到外部命令位置。
　　当外部命令执行时，会创建出一个子进程。这种操作被称为衍生。衍生过程需要花费时间和精力设置新子进程的环境。
　　内建命令和外部命令的区别在于前者不需要使用子进程来执行。他们已经和shell编译成了一体，作为shell工具的组成部分存在。不需要借助外部程序文件来运行。使用type命令可以了解某个命令是否是內建的。因为不需要衍生新子进程来执行，也不需要打开程序文件，內建命令的执行速度更快，效率更高。

	[root@localhost ~]# type -a echo
	echo is a shell builtin
	echo is /bin/echo
	[root@localhost ~]# which echo
	/bin/echo

　　type -a命令可以查出命令的两种实现，而which命令只显示外部命令文件。对于既是內建命令又是外部命令的命令，会默认使用內建命令，若想使用外部命令，直接指定对应文件即可。
　　history命令是一个有用的內建命令。

	history

　　bash shell会跟踪你用过的命令，要查看最近用过的命令列表，可以输入不带选项的history命令。通常历史记录中会保存最近的1000条命令。可以通过修改名为HISTORY的环境变量来设置记录的历史命令数。
　　输入！！，然后按回车键可以唤出刚刚用过的那条命令。
　　命令历史记录被保存在隐藏文件.bash_history中，它位于用户的主目录中。需要注意的是，bash命令的历史记录是现存放在内存中，当shell退出时才被写入历史文件中。可以通过history命令的-a选项来在退出shell会话之前强制将命令历史记录写入.bash_history文件。
　　可以通过惊叹号和命令在历史列表中的编号来唤出历史命令。
　　alias命令允许为常用命令（及其参数）创建另一个名称，从而将输入量减少到最低。

	alias

　　Linux发行版已经设置好了一些常用命令的别名。可以使用alias命令的-p选项来查看当前可用的别名。
　　当定义好别名后，随时可以在shell中使用，在shell脚本中也可以。但因为命令别名属于內建命令，一个别名只有在它所定义的shell进程中才有效。

#第六章 使用linux环境变量#

　　bash shell用一个叫环境变量的特性来存储有关shell会话和工作环境的信息。这种特性允许你在内存中存储数据，以便程序或shell中运行的脚本能够轻松访问它们。这也是存储持久数据的一种简便方法。
　　在bash shell中，环境变量分两类：

- 全局变量
- 局部变量

　　全局环境变量对于shell会话和所有生成的子shell都是可见的。局部环境变量只对创建它们的shell可见。全局环境变量可以帮助子shell获取父shell的信息。
　　系统环境变量基本上都是使用全大写字母，以区别于普通用户的环境变量。要查看全局变量，可以使用env或printenv命令。printenv命令可以用来查看个别环境变量。也可以使用echo来显示变量值，这是引用环境变量时，需要在变量前加上美元符（$）。

	[root@localhost ~]# env
	HOSTNAME=localhost.localdomain
	SELINUX_ROLE_REQUESTED=
	TERM=xterm
	SHELL=/bin/bash
	HISTSIZE=1000
	[...]
	HOME=/root
	[...]
	_=/bin/env
	[root@localhost ~]# printenv HOME
	/root
	[root@localhost ~]# env HOME
	env: HOME: 没有那个文件或目录
	[root@localhost ~]# echo $HOME
	/root
	[root@localhost ~]# ls $HOME
	anaconda-ks.cfg  install.log  install.log.syslog  sl_ins  sl_ins2  test  test1  test_hl  test_sl
	[root@localhost ~]# ls /root
	anaconda-ks.cfg  install.log  install.log.syslog  sl_ins  sl_ins2  test  test1  test_hl  test_sl
	[root@localhost ~]# bash
	[root@localhost ~]# ps -f
	UID        PID  PPID  C STIME TTY          TIME CMD
	root      2145  2140  0 10:04 pts/0    00:00:00 -bash
	root      2182  2145  0 10:07 pts/0    00:00:00 bash
	root      2193  2182  4 10:07 pts/0    00:00:00 ps -f
	[root@localhost ~]# echo $HOME
	/root
	[root@localhost ~]# exit
	exit
	[root@localhost ~]# 

　　在linux系统中没有仅显示局部环境变量的命令。set命令会显示某个特定进程设置的所有环境变量，包括局部变量、全局变量以及用户定义变量。

	[root@localhost ~]# set
	BASH=/bin/bash
	[...]
	BASH_ALIASES=()
	BASH_ARGC=()
	BASH_ARGV=()
	BASH_CMDS=()
	BASH_LINENO=()
	BASH_SOURCE=()
	[...]
	colors=/etc/DIR_COLORS
	my_variable='Hello World'
	[root@localhost ~]# 

　　set命令会按照字母顺序对字母进行排序，而env和printenv命令则不会。