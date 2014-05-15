Markdown学习笔记
====================
windows下vim编辑markdown
---------------------
1. 安装 [python for windwos环境](http://www.python.org/getit/releases/2.7.3/). 
	默认安装在c:\python27目录下,默认安装即可
2. 安装[Markdown-2.0.win32.exe](http://pypi.python.org/packages/any/M/Markdown/Markdown-2.0.win32.exe)
3. 安装配置vim或者gvim 
>noremap <F8> :!cmd /c c:\Python27\python c:\Python27\scripts\markdown.py %:t -e chinese > %:r.html<CR> 
>noremap <F12>  :!cmd /c start ./%:r.html<CR> 
>F8 编译 <F12> 查看编译后文件

markdown[快速入门](http://wowubuntu.com/markdown/basic.html)，[完整语法说明](http://wowubuntu.com/markdown/)
# Header 1
## Header 2
### Header 3
#### Header 4
##### Header 5
###### Header 6

>>> This is a blockquote.
> 
>> This is the second paragraph in the blockquote.
>
> ## This is an H2 in a blockquote

1. a
2. b
3. c
Some of these words *are emphasized*.
Some of these words _are emphasized also_.
Use two asterisks for **strong emphasis**.
Or, if you prefer, __use two underscores instead__.

I get 10 times more traffic from [Google][1] than from
[Yahoo][2] or [MSN][3].

[1]: http://google.com/ "Google"
[2]: http://search.yahoo.com/ "Yahoo Search"
[3]: http://search.msn.com/ "MSN Search"
This is an [example link](http://example.com/ "With a Title").
