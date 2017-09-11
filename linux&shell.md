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
　　一旦启动bash shell（或执行一个shell脚本），就能够创建在这个shell进程内可见的局部变量了。可以通过等号给环境变量赋值，值可以是数值或字符串。若要给变量赋一个含有空格的字符串，必须用引号来界定字符串的首尾。若没有使用引号，bash shell会认为下一个词是另一个要执行的命令。另外为作区分，自己创建的局部变量或是shell脚本中，一般使用小写字母。

	[root@localhost ~]# echo $my_variable
	
	[root@localhost ~]# my_variable=Hello
	[root@localhost ~]# echo $my_variable
	Hello
	[root@localhost ~]# my_variable=Hello World
	-bash: World: command not found
	[root@localhost ~]# my_variable="Hello World"
	[root@localhost ~]# echo $my_variable
	Hello World
	[root@localhost ~]# bash
	[root@localhost ~]# echo $my_variable
	
	[root@localhost ~]# my_child_variable="Hello Child World"
	[root@localhost ~]# exit
	exit
	[root@localhost ~]# echo $my_child_variable

	[root@localhost ~]# 

　　从上例可知，在子进程中设置的局部变量，一旦退出子进程，这个局部环境变量就不可用了。
　　创建全局环境变量的方法是先创建一个局部环境变量，然后再把它导出到全局变量中。这个过程通过export命令来完成，变量名前面不需要加＄。

	[root@localhost ~]# my_variable="i'm Global now"
	[root@localhost ~]# echo $my_variable
	i'm Global now
	[root@localhost ~]# export my_variable
	[root@localhost ~]# bash
	[root@localhost ~]# echo $my_variable
	i'm Global now
	[root@localhost ~]# my_variable="Null"
	[root@localhost ~]# echo $my_variable
	Null
	[root@localhost ~]# exit
	exit
	[root@localhost ~]# echo $my_variable
	i'm Global now
	[root@localhost ~]# bash
	[root@localhost ~]# my_variable="Null"
	[root@localhost ~]# export my_variable
	[root@localhost ~]# echo $my_variable
	Null
	[root@localhost ~]# exit
	exit
	[root@localhost ~]# echo $my_variable
	i'm Global now
	[root@localhost ~]# 

　　从上例可知，全局变量在子进程中可用，但是在子进程中修改后不会影响父shell中全局变量的值，使用export命令也无法影响。
　　unset命令可以删除已存在的环境变量。引用环境变量时，不加＄。同样，在子进程中删除全局变量不会影响父shell中全局变量的值。

	[root@localhost ~]# echo $my_variable
	i'm Global now
	[root@localhost ~]# unset my_variable
	[root@localhost ~]# echo $my_variable
	
	[root@localhost ~]# 

　　当在sehll命令行界面中输入一个外部命令时，shell会搜索系统来找到对应的程序。PATH环境变量定义了用于进行命令和程序查找的目录。PATH中的目录使用冒号分隔。若命令或程序的位置没有包括在PATH变量中，那么如果不使用绝对路径的话，shell是没法找到的。此时，shell会产生一个错误信息。
　　应用程序放置可执行文件的目录加入PATH环境变量后，就可以在虚拟目录结构中的任何位置执行程序。添加时无需从头定义，只需引用原来的PATH值，然后追加在后面即可。
　　通常可以将单点符（.）加入PATH环境变量，该单点符代表当前目录。
　　对PATH变量的修改只能持续到退出或重启系统。
　　在登入linux系统启动一个bash shell时，默认情况下bash会在几个文件中查找命令。这些文件叫做启动文件或环境文件。bash检查的启动文件取决于你启动bash shell的方式。启动bash shell有3中方式：

- 登录时作为默认登录shell
- 作为非登录 shell的交互式shell
- 作为运行脚本的非交互shell

　　当登录linux系统时，bash shell会作为登录shell启动。登录shell会从5个不同的启动文件中读取命令：

- /etc/profile
- $HOME/.bash_profile
- $HOME/.bashrc
- $HOME/.bash_login
- $HOME/.profile

　　/etc/profile文件是系统默认的bash shell的主启动文件。系统上每个用户登录时都会执行这个启动文件。另外4个启动文件是针对用户的，可根据个人需求定制。
　　当bash shell不是登录系统时启动的，那么该sehll叫做交互式shell。交互式shell不会像登录shell一样运行，但它依然提供了命令行提示符来输入命令。交互式shell启动时，不会访问etc/profile文件，只会检查用户HOME目录中的.bashrc文件。
　　.bashrc文件由两个作用：一是查看/etc目录下通用的bashrc文件，二是为用户提供一个定制自己的命令别名和私有脚本函数的地方。
　　系统执行shell脚本时启动的shell是非交互式的。它不提供命令行提示符。当sehll启动一个非交互式shell进程时，它会检查BASH_ENV环境变量来查看要执行的启动文件。如果有指定文件，shell会执行该文件里的命令，通常包括sehll脚本变量设置。
　　如果变量BASH_ENV没有设置，子shell会继承父shell导出过的变量。通常，父shell是登录shell，在/etc/profile、/etc/profile.d/*.sh和$HOME/.bashrc文件中设置并导出了变量，用于执行脚本的子shell就能继承这些变量。由父shell设置但并未导出的变量就是局部变量。子shell无法继承局部变量。而对于不启动子shell的脚本，变量已经存在于当前shell中，可以使用当前shell的局部变量和全局变量。
　　可以通过在/etc/profile文件中添加全局变量来持久化设置全局变量，但是当升级了所用发行版时，这个文件也会跟着更新，个人定制的变量设置就消失了。所以最好是在/etc/profile.d目录下创建一个以.sh结尾的文件。把所有新的货修改过的全局变量设置在这个文件中。
　　在大多数发行版中，存储个人用户永久性bash shell变量的地方是$HOME/.bashrc文件。但如果设置了BASH_ENV变量，它指向的不是$HOME/.bashrc，则需要在对应位置设置变量。
　　环境变量还可以作为数组使用。要给某个环境变量设置多个值，可以把值放在括号里，值与值之间用空格分隔。当引用单独的数组元素时，必须使用索引值。索引值用方括号括起来。可以使用通配符来显示多个数组变量。可以用索引值来设置某个数组元素值。可以使用unset命令删除某个或某些值。

	[root@localhost ~]# mytest=(one two three four five)
	[root@localhost ~]# echo $mytest
	one
	[root@localhost ~]# echo ${mytest[2]}
	three
	[root@localhost ~]# echo ${mytest[*]}
	one two three four five
	[root@localhost ~]# mytest[2]=seven
	[root@localhost ~]# echo ${mytest[*]}
	one two seven four five
	[root@localhost ~]# unset mytest[2]
	[root@localhost ~]# echo ${mytest[*]}
	one two four five
	[root@localhost ~]# echo ${mytest[2]}
	
	[root@localhost ~]# echo ${mytest[3]}
	four
	[root@localhost ~]# 

# 理解Linux文件权限 #

　　缺乏安全性的系统不是完整的系统。系统中必须有一套能够保护文件免遭非授权用户浏览和修改的机制。Linux沿用了Unix文件权限的办法，即允许用户和组根据每个文件和目录的安全性设置来访问文件。
　　Linux安全系统的核心是用户账户。每个能进入Linux系统的用户都会被分配唯一的用户账户。用户对系统中各种对象的访问权限取决于他们登录系统时用的用户。
　　用户权限是通过创建用户时分配的用户ID（UserID，通常缩写为UID）来跟踪。UID是数值，每个用户都有唯一的UID，但在登录系统时使用的登录名。登录名是用户用来登录系统的最长八字符的字符串（字符可以是数字或字母），同时会关联一个对应的密码。Linux系统使用特定的文件和工具来跟踪和管理系统上的用户账户。
　　Linux系统使用一个专门的文件来将用户的登录名匹配到对应的UID值。这个文件就是/etc/passswd文件，它包含了一些与用户有关的值。
　　root用户账户是Linux系统管理员，固定分配给他的UID是0，Linux系统还未各种功能创建了用户账户，这些账户并不是真的用户，这些账户叫做系统账户，是系统上运行的各种服务进程访问资源用的特殊用户。所有运行在后台的服务都需要一个系统用户账户登录到Linux系统上。如果让这些服务用root账户登录，有非授权的用户攻陷其中一个服务后，就可以作为root用户访问整个系统。
　　Linux系统为系统账户预留了500一下的UID值。有些服务甚至必须使用特定的UID才能正常工作。为普通用户创建账户时，大多数Linux系统会从500开始，将第一个可用的UID分配给这个账户。
　　在/etc/passwd/文件中还有很多用户登录名和UID之外的信息，包括：

- 登录用户名
- 用户密码
- 用户账户的UID（数字形式）
- 用户账户的组ID（数字形式）
- 用户账户的文本描述（称为备注字段）
- 用户HOME目录的位置
- 用户默认shell

　　其中密码字段全部显示x，鉴于很多程序都需要访问/etc/passwd文件获取用户信息，以及破解加密密码的工具不断演进，所以绝大多数的Linux系统都将用户密码保存在另一个单独的文件，称为shadow文件，位置为/etc/shadow。这个文件对Linux系统密码管理提供了更多的控制。只有root用户才能访问/etc/shadow文件。它为系统上每个用户账户都保存了一条记录。包括9个字段：

- 与/etc/shadow文件中的登录名字段对应的登录名
- 加密后的密码
- 自上次修改密码后过去的天数密码（自1970年1月1号开始计算）
- 多少天后才能更改密码
- 多少天后必须更改密码
- 密码过期前提前多少天提醒用户更改密码
- 密码过期后多少天禁用用户账户
- 用户账户被禁用的日期（用自1970年1月1号到当天的天数表示）
- 预留字段给将来使用

　　useradd命令用来向Linux系统添加新用户。可以一次性创建新用户账户及设置用户HOME目录结构。useradd命令使用系统默认值以及命令行参数来设置用户账户。系统默认值被设置在/etc/default/useradd文件中。可以使用加入了-D选项的useradd命令查看所用Linux系统中的这些默认值。

	[root@localhost ~]# useradd -D
	GROUP=100
	HOME=/home
	INACTIVE=-1
	EXPIRE=
	SHELL=/bin/bash
	SKEL=/etc/skel
	CREATE_MAIL_SPOOL=yes
	[root@localhost ~]# 

　　这些默认值的含义为：

- 新用户会被添加到GID为100的公共组
- 新用户的HOME目录将位于/home/loginname
- 新用户账户密码在过期后不会被禁用
- 新用户账户未设置过期日期
- 新用户账户将bash shell作为默认shell
- 系统会将/etc/skel目录下的内容复制到用户的HOME目录下
- 系统为该用户账户在mail目录下创建一个用于接收邮件的文件

　　倒数第二个值允许管理员创建一份默认的HOME目录配置，然后把它作为创建新用户HOME目录的模板。这样就能自动在每个新用户的HOME目录放置默认的系统文件。
　　在创建用户时可以使用参数改变默认值或默认行为，这些参数有：

	  参数                                 描述
	-c comment                     给新用户添加备注
	-d home_dir                    为主目录指定一个名字（如果不想用登录名作为主目录名的话）
	-e expire_data                 用YYYY-MM-DD格式指定一个账户过期的日期
	-f inactive_days               指定这个账户密码过期多少天后这个账户被禁用；0表示过期马上禁用；-1表示禁用这个功能，即过期不禁用
	-g initial_group               指定用户登录组的GID或组名
	-G gruop ...                   指定用户除登录组之外所属的一个或多个附加组
	-k                             必须和-m一起使用，将/etc/skel目录的内容复制到用户的HOME目录
	-m                             创建用户的HOME目录
	-M                             不创建用户的HOME目录（只有当默认设置中要求创建时才使用这个选项）
	-n                             创建一个与用户登录名同名的新组
	-r                             创建系统账户
	-p passwd                      为用户账户指定默认密码
	-s shell                       指定默认登录的shell
	-u uid                         为账户指定唯一的UID

　　可以在-D选项后加上指定的值来修改系统默认的新用户设置，这些参数有：

	  参数                                 描述
	-b default_home                更改默认的创建用户HOME目录的位置
	-e expiration_date             更改默认的新账户的过期日期
	-f inactive                    更改默认的新用户从密码过期到账户被禁用的天数
	-g group                       更改默认的组名称或GID
	-s shell                       更改默认的登录shell

　　userdel命令可以从系统中删除用户，但默认情况下他只会删除/etc/passwd文件中的用户信息，而不会删除系统中属于该账户的任何文件。加上-r参数则会删除该用户的HOME目录以及邮件目录，然而系统上仍可能存在已删除用户的其他文件。

	userdel -r

　　usermod命令是修改用户账户工具中最强大的一个。他能用来修改/etc/passwd文件中的大部分字段，只需用对应的命令行参数即可。参数大部分跟useradd命令的参数一致。

	usermod

- -c 修改备注字段
- -e 修改过期日期
- -g 修改默认的登录组
- -l 修改用户账户的登录名
- -L 锁定账户，使用户无法登录
- -p 修改账户密码
- -U 解除锁定，是用户能够登录

　　passwd命令是改变用户密码的简便方法。系统上任何用户都可以改自己的密码，但只有root用户才有权限修改别人的密码。

	passwd

　　-e选项可以强制用户下次登录时修改密码。
　　chpasswd命令适用于需要为系统中大量用户修改密码的情况。它可以从标准输入自动读取登录名和密码对（由冒号分隔）列表，给密码加密，然后为用户账户设置。也可以用重定向命令来将含有userid:passwd对的文件重定向给该命令。

	chpasswd < users.txt

　　chsh命令用来快速修改默认的用户登录shell。使用时必须用shell的全路径名作为参数，不能只用shell名。

	chsh

　　chfn命令提供了在/etc/passwd文件的备注字段中存储信息的标准方法。当没有参数时，他会询问要将哪些适合的内容加入备注字段。

	chfn

　　change命令可以用来帮助管理用户账户的有效期。参数有：

- -d 设置上次修改密码到现在的天数
- -E 设置密码过期的日期
- -I 设置密码过期到锁定账户的天数
- -m 设置修改密码之间最少要多少天
- -W 设置密码过期前多久开始出现提醒信息

　　change命令的日期值可以用以下两种形式：

- YYYY-MM-DD格式日期
- 代表从1970年1月1日到该日期天数的数值

　　change命令可以用来创建在特定日期自动过期的临时用户，过期账户和锁定账户相似，账户存在但无法登录。

	change

　　用户账户在控制单个用户安全性方便很好用，但在涉及共享资源的一组用户时就力不从心了。未解决这个问题，Linux系统采用了另一个安全概念————组。
　　组权限允许多个用户对系统中的对象（比如文件、目录和设备等）共享一组公用的权限。
　　每个组都有唯一的GID，在系统上是唯一的数值。除了GID，每个组还有唯一的组名。
　　与用户账户类似，组信息也保存在系统的一个文件中。/etc/group文件包含系统上用到的每个组的信息。
　　与UID类似，GID在分配时也采用了特定的格式。系统账户用的组通常会分配低于500的GID值，而用户组的GID则会从500开始分配。/etc/group文件有4个字段：

- 组名
- 组密码
- GID
- 属于改组的用户列表

　　禁止通过直接修改/etc/group文件来添加用户到一个组，应该用usermod命令。在添加用户到不同的组之前，首先要创建组。
　　当一个用户在/etc/passwd文件中指定某个组为默认组时，用户账户不会作为改组成员再出现在/etc/group文件中。
　　groupadd命令可以在系统上创建新组。但该命令没有提供将用户添加到组中的选项。usermod命令可以实现这一功能。usermod命令的-G选项会把这个新组添加到该用户账户的列表中。而-g选项则会替换该账户的默认组。

	groupadd

　　更改已登录系统账户的所属组，在该用户重新登录系统时，组关系更改才会生效。
　　使用groupmod命令可以修改已有组的GID（加-g选项）或组名（加-n选项）。

	groupmod

　　ls命令可以用来查看Linux系统上大的文件、目录和设备的权限。ls命令输出的第一个字段是描述文件和目录权限的编码。这个字段的第一个字符代表了对象的类型：

- -代表文件
- d代表目录
- l代表链接
- c代表字符型设备
- b代表块设备
- n代表网络设备

　　之后有3组三字符的编码。每一组定义了3种访问权限：

- r代表对象是可读的
- w代表对象是可写的
- x代表对象是可执行的

　　若没有相关权限，在该权限位会出现单破折号。这3组权限分别对应对象的3个安全级别：

- 对象的属主
- 对象的属组
- 系统其它用户

　　umask命令用来设置所创建文件和目录的默认权限。利用touch命令会用分配给该账户的默认权限创建文件。umask命令可以显示和设置这个默认权限。

	[root@localhost ~]# umask
	0022
	[root@localhost ~]# 

　　第一位代表一项特别的安全特性，叫做黏着位（sticky bit）。给可执行文件设置粘着位是为了提升性能，使其在进程结束后仍驻留在内存中，而给目录设置粘着位是为了实现“在公用目录,保证只有文件属主或者超级用户才有权利删除和更名，而其他用户不能删除和更名不属于他的文件”。
　　后面3位表示文件或目录对应的umask八进制值。
　　八进制模式的安全性设置会先获取3位rwx权限的值，然后将其转换为3位二进制值，用一个八进制数值来表示。下面列出可能出现的组合：

	 权 限        二进制值        八进制值        描 述
	  ---           000             0         没有任何权限
      --x           001             1         只有执行权限
      -w-           010             2         只有写入权限
      -wx           011             3         只有写入和执行权限
      r--           100             4         只有读取权限
      r-x           101             5         有读取和执行权限
      rw-           110             6         有读取和写入权限
      rwx           111             7         有全部权限

　　而umask值其实是掩码。也就是说要把umask值从对象的全权限值中减掉。对于文件来说，全权限是666，对于目录来说，则是777。所以默认touch命令创建的文件的默认权限是666减去022，也就是644。

	[root@localhost ~]# touch newfile
	[root@localhost ~]# ll newfile
	-rw-r--r--. 1 root root 0 9月   7 09:56 newfile
	[root@localhost ~]#

　　在大多数Linux发行版中，umask值通常会设置在/etc/profile启动文件中，有一些是设置在/etc/login.defs文件中的。可以用umask命令为默认umask设置指定的新值。
　　chmod命令可以用来改变文件和目录的安全性设置。该命令格式如下：

	chmod options mode file

　　mode参数可以使用八进制模式或符号模式进行安全性设置。
　　八进制模式设置非常直观，直接用期望赋予文件的标准3位八进制权限码即可。

	[root@localhost ~]# chmod 760 newfile
	[root@localhost ~]# ll newfile
	-rwxrw----. 1 root root 0 9月   7 09:56 newfile
	[root@localhost ~]# 

　　符号模式指定权限的格式为：

	[ugoa...][+-=][rwxXstugo...]

　　第一组字符定义了权限作用的对象：

- u代表用户
- g代表组
- o代表其他
- a代表上述所有

　　后面跟的符号表示是在现有权限基础上增加权限（+），还是在现有权限上移除权限（-），或是将权限设置为后面的值（=）。
　　最后，第三个符号代表作用到设置上的权限，除了通常的rwx，还有：

- X 如果对象是目录或其他用户有可执行权限时，赋予执行权限
- s 运行时重新设置UID或GID
- t 设置黏着位
- u 将权限设置为跟属主一样
- g 将权限设置为跟属组一样
- o 将权限设置为跟其他用户一样

	[root@localhost ~]# chmod o+r newfile
	[root@localhost ~]# ll newfile
	-rwxrw-r--. 1 root root 0 9月   7 09:56 newfile
	[root@localhost ~]# chmod u-x newfile
	[root@localhost ~]# ll newfile 
	-rw-rw-r--. 1 root root 0 9月   7 09:56 newfile
	[root@localhost ~]# chmod o=u newfile 
	[root@localhost ~]# ll newfile 
	-rw-rw-rw-. 1 root root 0 9月   7 09:56 newfile
	[root@localhost ~]# 

　　-R选项可以让权限的改变递归地作用到文件或目录。还可以使用通配符指定多个文件同意更改权限。
　　chown命令用来改变文件的属主，chgrp命令用来改变文件的默认属组。
　　chown命令的格式为：

	chown options [owner].[group] file
	chgrp group file
　　

	[root@localhost ~]# chown han newfile
	[root@localhost ~]# ll newfile 
	-rw-rw-rw-. 1 han root 0 9月   7 09:56 newfile
	[root@localhost ~]# chown han.power newfile
	[root@localhost ~]# ll newfile 
	-rw-rw-rw-. 1 han power 0 9月   7 09:56 newfile
	[root@localhost ~]# chown .root newfile
	[root@localhost ~]# ll newfile 
	-rw-rw-rw-. 1 han root 0 9月   7 09:56 newfile
	[root@localhost ~]# chown test. newfile
	[root@localhost ~]# ll newfile 
	-rw-rw-rw-. 1 test test 0 9月   7 09:56 newfile

　　-R选项配合通配符可以递归的改变子目录和文件的所属关系。-h选项可以改变改文件所有符号链接文件的所属关系。
　　只有root用户能够改变文件的属主。任何属主都可以改变文件的属组，但前提是属主必须是原属组和目标属组的成员。
　　创建新文件是，Linux会用默认的UID和GID给文件分配权限。想让其他人也能访问文件，要改变其他用户所在安全组的访问权限，要么就给文件分配一个包含其他用户的默认属组。如果想在大范围环境中创建文档并将文档与人共享，会粉繁琐。有一种简单的方法可以解决这个问题。
　　Linux还为每个文件和目录存储了3个额外的信息位：

- 设置用户ID（SUID）：当文件被用户使用时，程序会以文件属主的权限运行
- 设置组ID（SGID）：对文件来说，程序会以文件属组的权限运行；对目录来说，目录中创建的新文件会以目录的默认属组作为默认属组
- 黏着位：进程结束后文件还驻留在内存中

　　SGID为对文件共享非常重要。启用SGID位后，你可以强制在一个共享目录下创建的新文件都属于该目录的属组，这个组就成为了每个用户的属组。
　　SGID课通过chmod命令设置。他会加到标准3位八进制值之前（组成4位八进制值），或者在符号模式中使用符号s。
　　对于八进制模式下：

	二进制值        八进制值          描  述 
	  000             0           所有位都清零
	  001             1           黏着位置位
	  010             2           SGID位置位
	  011             3           SGID位和黏着位都置位
	  100             4           SUID位置位
	  101             5           SUID位和黏着位都置位
	  110             6           SUID位和SGID位都置位
	  111             7           所有位都置位

　　要创建一个共享目录，是目录中的新文件都沿用目录的属组，只需将该目录的SGID位置位。

	[root@localhost ~]# mkdir testdir
	[root@localhost ~]# ll
	drwxr-xr-x. 2 root root   4096 9月   7 11:12 testdir
	[root@localhost ~]# chgrp power testdir
	[root@localhost ~]# ll
	drwxr-xr-x. 2 root power  4096 9月   7 11:12 testdir
	[root@localhost ~]# chmod g+s testdir/
	[root@localhost ~]# ll
	drwxr-sr-x. 2 root power  4096 9月   7 11:12 testdir
	[root@localhost ~]# umask 002
	[root@localhost ~]# cd testdir/
	[root@localhost testdir]# touch tesfile
	[root@localhost testdir]# ll
	总用量 0
	-rw-rw-r--. 1 root power 0 9月   7 11:37 tesfile
	[root@localhost testdir]# 

　　首先，用mkdir命令创建希望共享的目录。然后通过chgrp命令将目录的默认属组改为包含有需要分享共享文件的用户的组（你也必须是该组的成员）。最后，将目录的SGID位置位，以保证目录中新建文件都用power作为默认属组。为了让这个环境正常工作，所有组成员都需要将他们的umask值设为文件对属组成员可写。在上例中，umask值改为002，所以文件对属组是可写的。

#第八章 管理文件系统#

　　Linux最初采用的是一种简单的文件系统，它模仿了Unix文件系统的功能。

###基本的Linux文件系统###

####ext文件系统####

　　Linux操作系统中引入的最早的文件系统叫做扩展文件系统（extend filesystem，简记为ext）。它使用Linux提供了一个基本的类Unix文件系统：使用虚拟目录来操作硬件设备，在物理设备上按定长的块来存储数据。
　　ext文件系统采用名为索引节点的系统来存放虚拟目录中所存储文件的信息。索引节点系统在每个物理设备中创建一个单独的表（称为索引节点表）来存储这些文件的信息。存储在虚拟目录中的每一个文件在索引节点表中都有一个条目。ext文件系统名称中extended部分来自其跟踪的每个文件的额外数据，包括：

- 文件名
- 文件大小
- 文件的属主
- 文件的属组
- 文件的访问权限
- 指向存有文件数据的每个硬盘块的指针

　　Linux通过唯一的数值（索引节点号）来引用索引节点表中的每个索引节点，这个值是创建文件时由文件系统分配的。文件系统通过索引号节点而不是文件全名及路径来标识文件。

####ext2文件系统####

　　最早的ext文件系统有不少限制，比如文件大小不得超过2GB。在Linux出现不久后，ext文件系统就升级到第二代扩展文件系统，叫做ext2。
　　ext2文件系统时ext文件系统基本功能的一个扩展，但保持了同样的结构。ext2文件系统扩展了索引节点表的格式来保存系统上的每个文件的更多信息。
　　ext2的索引节点表为文件添加了创建时间值、修改时间值后最后访问时间值来帮助系统管理员追踪文件的访问情况。ext2文件系统将允许的最大文件大小增加到2TB（在ext2的后期版本中增加到了32TB），以容纳数据库服务器中常见的大文件。
　　ext文件系统常见的问题是文件写入物理设备时，存储数据用的块很容易分散在整个设备中（称作碎片化，fragmentation）。数据块的碎片化会降低文件系统的性能，因为需要更长的时间在存储设备中查找特定文件的所有块。保存文件时，ext2文件系统通过按组分配磁盘块来减轻碎片化，通过将数据分组，文件系统在读取文件时就不需要为了数据块查找整个物理设备。
　　多年来，ext文件系统一直都是Linux发行版采用的默认文件系统。但它也有一些限制，索引节点表虽然支持文件系统保存有关文件的更多信息，但会对操作系统造成致命的问题。文件每次存储或更新文件，它都要用新信息来更新索引节点表。但若果计算机系统在存储文件和更新索引节点时发生意外，这两者的内容就不同步了，ext2文件系统由于容易在系统崩溃或断电时损坏而臭名昭著。

###日志文件系统###

　　日志文件系统会先将文件的更改写入临时文件（称为日志，journal）中。在数据成功写到存储设备和索引节点表之后，再删除对应的日志条目。若在写入存储设备之前崩溃或断电，日志文件系统下次会读取日志文件并处理上次留下的未写入的数据。
　　Linux中有3中广泛使用的日志方法，每种的保护等级都不相同：

- 数据模式：索引节点和文件都会被写入日志；丢失数据风险低，但性能差
- 有序模式：只有索引节点数据会被写入日志，但只有数据成功写入后才删除；在性能和安全性之间取得了良好的折中
- 回写模式：只有索引节点数据会被写入日志，但不控制文件数据何时写入；丢失数据风险高，但仍比不用日志好

　　数据模式日志方法是目前为止最安全的数据保护方法，但同时也是最慢的。所有写到存储设备上的数据都必须写入两次：第一次写入日志，第二次写入真正的存储设备。这样会导致性能很差，尤其对于要做大量数据写入的系统而言。

####ext3文件系统####

　　2001年，ext3文件系统被引入Linux内核，知道最近几乎所有Linux发行版默认的文件系统。它采用和ext2文件系统相同的索引节点表结构，但给每个存储设备增加了一个日志文件，将准备写入存储设备的数据先记入日志。
　　默认情况下，ext3文件系统用有序模式的日志功能————直将索引节点信息写入日志文件，知道数据块都被成功写入存储设备才删除。在创建文件系统时可以用简单的一个命令行选项将ext3文件系统的日志方法改成数据模式或回写模式。
　　但是，ext3文件系统无法恢复误删的文件，他没有任何內建的数据压缩功能（有个需要单独安装的补丁支持该功能），ext3文件系统也不支持加密文件。

####ext4文件系统####

　　ext4文件系统在2008年受到Linux内核官方支持，现在已是大多数流行的Linux发行版采用的默认文件系统，如Ubuntu。
　　除了支持数据压缩和加密，ext4文件系统还支持一个称作区段（extent）的特性。区段在存储设备上按块分配空间，但在索引节点表中只保存起始块的位置。由于无需列出所有用来存储文件的数据块，可以在索引节点表中节省一些空间。
　　ext4文件系统还引入了块预分配技术（block preallocation）。若想在存储设备上请求一个会变大的文件空间，ext4文件系统会分配所有需要用到的块，而不仅仅目前用到的块。ext4文件系统会用0填满预留的数据块，不会把它们分配给其他文件。


####Reiser文件系统####

　　2001年，Hans Reiser为Linux系统创建了第一个日志文件系统，称为ReiserFS。该系统只支持回写日志模式————只讲索引节点表数据写入日志文件。它也因此称为Linux系统最快的文件系统之一。
　　ReiserFS文件系统可以在线调整已有文件系统的大小，还支持一个称为尾部压缩（tailpacking）的技术，该技术能将一个文件的数据填进另一个文件的数据块中的空白空间。当需要为已有文件系统扩容来容纳更多数据时，在线调整文件系统大小功能非常好用。

####JFS文件系统####

　　作为可能依然在用的最老的日志文件系统之一，JFS（Journaled File System）文件系统是IBM在1990年为其Unix衍生版AIX开发的。直到第2版，它才被移植到Linux系统。IBM官方称其为JFS2，单大多数Linux系统提到它时只用JFS。
　　JFS文件系统采用的是有序日志方法，即只在日志中保存索引节点表数据，直到真正的文件数据被写入存储设备时才删除它。这个方法是ReiserFS的速度和数据模式日志方法的完整性之间的一种折中。
　　JFS文件系统采用基于区段的文件分配，即为每个写入存储设备的文件分配一组块。这样可以减少存储设备上的碎片。除了IBM Linux上外，JFS文件系统并没有流行起来。

####XFS文件系统####

　　XFS日志文件系统也是最初用于商业Unix系统而如今走进Linux世界的文件系统。美国硅图公司（SGI）最初在1994年为其商业化的IRIX系统开发了XFS。2002年它被发布到了适用于Linux环境的版本。
　　它采用回写模式的日志，在提供了高性能的同时也引入了一定的风险，因为实际数据并未存入日志文件。XFS文件系统还允许在线调整文件系统的大小，不同于ReiserFS文件系统，它只能扩大不能缩小。

###写时复制文件系统###

　　采用日志式技术就必须在安全性和性能之间做出选择。
　　就文件系统而言，日志式的另一种选择是写时复制（copy-on-write，COW）的技术。COW利用快照兼顾了安全性和性能。若要修改数据，会使用克隆或可写快照。修改过的数据并不会直接覆盖当前数据，而是被放入文件系统中的另一个位置。即便数据修改已完成，之前的旧数据也不会被重写。

####ZFS文件系统####

　　该系统是有Sun公司于2005年研发的，用于OpenSolaris操作系统，从2008年开始向Linux移植，最终在2012年投入Linux产品的使用。
　　ZFS是一个稳定的文件系统，与Reiser4、Btrfs和ext4势均力敌。它最大的弱项是没有使用GPL许可，以致无法成为Linux默认的文件系统。自2013年发起的OpenZFS项目有可能改变这个局面。

####Btrfs文件系统####

　　该系统是COW的新人，也被称为B树文件系统。它由oracle公司于2007年开始研发的。Btrfs在Reiser4的诸多特性的基础上改进了可靠性。另一些开发人员最终也加入开发过程，帮助Btrfs快速成为最流行的文件系统。究其原因，归功于它的稳定性、易用性以及能够动态调整已挂载文件系统的大小。OpenSUSE Linux发行版最近将Btrfs作为默认文件系统。此外，它也出现在其他Linux发行版中（如RHEL），不过不是默认文件系统。

##操作文件系统##

　　Linux系统提供了一些不同的工具来在命令行中进行文件系统的操作。可以对心所欲地创建新的文件系统或修改已有的文件系统。

###创建分区###

　　fdisk工具用来帮助管理安装在系统上的任何存储设备上的分区。它是个交互式程序，允许输入命令来逐步完成磁盘分区操作。
　　要启动fdisk命令，不许指定要分区的存储设备的设备名，另外还要有超级用户权限。若没有对应权限，会报出如下错误：

	[test@localhost ~]$ fdisk /dev/sdb
	
	Unable to open /dev/sdb
	[test@localhost ~]$ 

　　有时候，创建新磁盘分区最麻烦的事情就是找出安装在Linux系统中的物理磁盘。Linux采用了一种标准格式来为磁盘分配设备名称。对于老式的IDE驱动器，Linux使用的是/dev/hdx。其中x表示一个字母，具体是什么要根据驱动器的检测顺序（第一个驱动器是a，第二个驱动器是b，以此类推）。对于比较新的SATA驱动器和SCSI驱动器，Linux使用/dev/sdx。其中的x具体是什么也要根据驱动器的检测顺序（第一个驱动器是a，第二个驱动器是b，以此类推）。在格式化分区之前，最好再检测一下是否争取确定了驱动器。
　　如果拥有了超级用户权限并指定了正确的驱动器，那就可以进入fdisk工具的操作界面了。

	[root@localhost dev]# fdisk sdb
	
	WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
	         switch off the mode (command 'c') and change display units to
	         sectors (command 'u').
	
	Command (m for help): 

　　fdisk交互式命令提示符使用单字母命令来告诉fdisk做什么。下面为fdisk命令提示符下可用的命令：

- a：设置活动分区标志
- b：编辑BSD Unix系统用的磁盘标签
- c：设置DOS兼容标志
- d：删除分区
- l：显示可用的分区类型
- m：显示命令选项
- n：添加一个新分区
- o：创建DOS分区表
- p：显示当前分区表
- q：退出，不保存更改
- s：为Sun Unix系统创建一个新磁盘标签
- t：修改分区的系统ID
- u：改变使用的存储单位
- v：验证分区表
- w：将分区表写入磁盘
- x：高级功能

　　实际日常工作中只会用到几个基本命令。
　　对于初学者，可以用p命令将一个存储设备的详细信息显示出来。

	Command (m for help): p

	Disk sdb: 1073 MB, 1073741824 bytes
	255 heads, 63 sectors/track, 130 cylinders
	Units = cylinders of 16065 * 512 = 8225280 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disk identifier: 0xe18f4e2a
	
	Device Boot      Start         End      Blocks   Id  System
	
	Command (m for help):

　　显示这个存储设备有1073MB（1GB）的空间。存储设备明细后的列表说明这个设备上是否已有分区。这个例子中还没有分区。
　　使用n命令可以在该存储设备上创建新的分区。

	Command (m for help): n
	Command action
	   e   extended
	   p   primary partition (1-4)
	p  
	Partition number (1-4): 1
	First cylinder (1-130, default 1): 1
	Last cylinder, +cylinders or +size{K,M,G} (1-130, default 130): 1G
	
	Command (m for help): p
	
	Disk sdb: 1073 MB, 1073741824 bytes
	255 heads, 63 sectors/track, 130 cylinders
	Units = cylinders of 16065 * 512 = 8225280 bytes
	Sector size (logical/physical): 512 bytes / 512 bytes
	I/O size (minimum/optimal): 512 bytes / 512 bytes
	Disk identifier: 0xe18f4e2a
	
	Device Boot      Start         End      Blocks   Id  System
	  sdb1               1           1        8001   83  Linux
	
	Command (m for help): 

　　分区可以按主分区（primary partition）或扩展分区（extended partition）创建。主分区可以被文件系统直接格式化，而扩展分区则只能容纳其他住分区。扩展分区出现的原因是每个存储设备上只能由4个分区。可以通过扩展多个扩展分区，然后在扩展分区内创建主分区进行扩展。上例中创建了一个主分区，在存储设备上给它分配了分区号1，然后给它分配了1GB的存储设备空间。
　　该存储设备上有了一个分区（/dev/sdb1）。Id列定义了Linux怎样对待该分区。fdisk允许创建多种分区类型。使用l命令可出可用的不同类型。默认类型是83，该类型定义了一个Linux文件系统。若为其他文件系统创建分区（如Windows的NTFS分区），只要选择一个不同的分区类型即可。创建分区后，用w命令将更改保存到存储设备上。

	Command (m for help): w
	The partition table has been altered!
	
	Calling ioctl() to re-read partition table.
	Syncing disks.
	[root@localhost dev]# 

　　存储设备的分区信息写入分区表中，Linux系统通过ioctl()调用来获知新分区的出现。设置好分区后，可以用Linux文件系统对其进行格式化。