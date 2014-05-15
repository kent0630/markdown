Markdown学习笔记
=======================
##1.概述
- 纯文本，易书写，易版本控制，跨平台
- 专注内容书写，排版通过转换成标记语言来实现
- [markdown项目首页](http://daringfireball.net/projects/markdown/)

##2.基本语法
- 完全兼容HTML语法
- [语法说明完整版（简体中文）](http://wowubuntu.com/markdown/index.html#editor)
- 关于代码模块的扩展语法(无法显示完整语法的，参见本文的markdown源码)  
**方式一**
    
        ```python  
            class SomeClass:
                pass
            if __name__ == '__main__':
                 print 'hello world'
        ``` 
 **方式二** 
    
        ``` 
            class SomeClass:
                pass
            if __name__ == '__main__':
                print 'hello world'
        ```
        {.python}
    
##3.工具

####在线编辑器
- [Mahua在线](http://mahua.jser.me/)
	- 输出支持代码高亮
	- 自定义css,并提供多款css可导出
	- 支持vim快捷键
- [dillinger](http://dillinger.io/)
	- HTML5编辑器
	- Dropbox
- 官方转化工具[Dingus](http://daringfireball.net/projects/markdown/dingus)

####mac下的工具
- Byword
	- 支持MultiMarkdown语法
	- 导出格式多，HTML，Word，PDF，RTF，Latax
	- 有方便的快捷键
- [Marked](http://marked2app.com/)
	- 纯预览工具，实时监控文档变化，配合Byword或者VIM使用很完美
	- 多种css选择
    - 可以支持数学公式
    - 支持程序语法高亮
-  [mou](http://mouapp.com/) 
	- 两栏界面，适时预览
	- 还不是正式版，免费，发展中
- MarkdownPro	
- [Markdown Service Tools](http://brettterpstra.com/code/?did=29)
- MacVIM  
	- 调用Marked作为预览工具，在vim配置文件中加入：

			:nnoremap <leader>m :silent !open -a Marked.app '%:p'<cr>

####windows工具(@TODO)
- [MarkdownPad](http://markdownpad.com/)
	- 基于.NetFramework4.0
- [Markpad](http://code52.org/DownmarkerWPF/)
- [MEditor](https://github.com/5d13cn/MEditor)
- Vim for win
	1. 安装 [python for windwos环境](http://www.python.org/getit/releases/2.7.3/). 
	默认安装在c:\python27目录下,默认安装即可
	2. 安装[Markdown2.0.win32.exe](http://pypi.python.org/packages/any/M/Markdown/Markdown-2.0.win32.exe)
	3. 安装配置vim或者gvim

			noremap <F8> :!cmd /c c:\Python27\python c:\Python27\scripts\markdown.py %:t -e chinese > %:r.html<CR>
			noremap <F12>  :!cmd /c start ./%:r.html<CR> 
		*F8* 编译    
		*F12* 查看编译后文件


>参考：[关于MultiMarkdown的使用和说明](http://fletcherpenney.net/multimarkdown/)

---

####修订记录
- 20120917 初稿
- 完全兼容HTML语法 
- 20140104 增加马克飞象、补充Marked2、code语法
