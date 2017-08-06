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