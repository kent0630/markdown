VIM/GVIM学习笔记 
===================
##基本使用
####基本操作
- *5dd* 从当前行开始删除5行
- *cc* 删除当前行并且进入插入模式
- *5yy* 从当前行开始拷贝5行
- *1,3d* 删除1至3行
- *1,3y* 拷贝1至3行 （.代表当前行，$代表最后一行）
- *:<C\-F>* 历史命令记录的窗口
- *:Explore*或*E* 打开文件浏览器
- *<C\-G>* 光标所在位置的行数和列数报告
- *D* 删除到行尾
- *:x* 如果修改则保存
- *set rnu* 显示相对行号
- *u* 撤销，*<C\-R>* 重做
- *\.* 重做上一个命令

####光标移动
- <s>zz 让光标所杂的行居屏幕中央</s>
- <s>zt 让光标所杂的行居屏幕最上一行 t=top</s>
- <s>zb 让光标所杂的行居屏幕最下一行 b=bottom</s>
- *H*,*L*,*M* 控制光标移动到当前屏幕头屏幕尾和屏幕中
- *nG* 跳转命令。n为行数，该命令立即使光标跳到指定行
- *w* , *b* 光标向前向后跳转一个单词
- *N|* 光标到第N列
- *gg* 到文件第一行
- *G* 到文件最后一行
- *<C\-]>* 链接跳转
- *<C\-T>*,*<C\-O>* 链接跳转和跳回

####滚动
- 整页翻页*<C\-F><C\-B>* F就是Forword B就是Backward
- 翻半页*<C\-D><C\-U>*   D=down U=up
- `:set scrolloff=2` 上下移动光标时, 始终保持光标上或下有两行在屏幕上.

####窗口
- *<C\-W> h，<C\-W> j，<C\-W> k，<C\-W> l* 切换到左下上右窗口
- *:split* 文件名（开启另一个窗口察看指定文件）:new 开新窗口新建文件
- *:vsplit* 文件名（开启另一个窗口察看指定文件）:vnew 开新窗口新建文件
- *:only* 只保留当前窗口
- *:close* 关闭窗口，可防止最后一个窗口时退出vim

####标签页
- *:tabe*新建一个标签页。
- *:tabn*(*gt*) \\ *:tabp*(*gT*) 切换到下一个\\上一个标签页。
- *:close* 关闭当前标签页。
- *:qa* 关闭所有标签页退出。
- *:tabdo*+命令 在所有的标签页中执行指定命令  

####替换与查找
- 替换查找*%s/word1/word2/g*
- *\** 转到当前光标所指的单词下一次出现的地方,然后可以通过 *n* 继续选择
- *\#* 转到当前光标所指的单词上一次出现的地方
- *g\*,g\#* 与以上功能类似，但也查找部分配配

##高级技巧
####多文件编辑
- *:args* 查看文件列表
- *:\(2\)n\(ext\)*编辑下一文件，并且可以在前面计数
- *:p\(revious\)*编辑上一文件
- *:first :last*  跳转到第一个或者最后一个文件
- *<C\-^>*在文件列表中的两个文件间跳转
- *:args file1\.c file2\.c file3\.h* 打开另一个文件列表
- 一般情况下，如果当前文件没保存，需要保存他，或者在args后加  \! 放弃保存  
当然也可以设置*:set autowrite* 自动保存，或者*:set noautowrite*关闭自动保存

####MARK
- *m a* 定义标记a
- *'a* 跳转到定义过的标记a
- *:marks a* 列出标记a，缺省参数列出所有的位置标记
- *:delm\!* 删除所有标记，*delm a* 删除标记a
- 标记类别：  
	- 'a - 'z  小写位置标记，在每个文件内有效。  
	- 'A - 'Z  大写位置标记，也叫做文件标记，在文件间都有效。  
	- '0 - '9  数字位置标记，在 \.viminfo 文件里设置。  

- 当你跳转到另一个文件后，有两个预定义的标记非常有用:  
	- *\`"* 这个标记使你跳转到你上次离开这个文件时的位置
	- *\`.* 标记记住你最后一次修改文件的位置

文件间拷贝文本，由于windows下开启了剪贴板共享，所以暂时不学习
共享剪贴板也有不便之处

####寄存器使用
- 可参考帮助:help v\_p
- *:reg* 查看当前寄存器
- 使用计数器前调用"< register>
- "< register>dd 将删除的行存到指定寄存器中
- 2,4y < register> 将2-4行复制到制定寄存器中

- 计数器分类和主要计数器：
	1. 无名寄存器 ""
	2. 10 个编号寄存器 "0 到 "9
	3. 行内删除寄存器 "\-
	4. 26 个命名的寄存器 "a 到 "z 或者 "A 到 "Z
	5. 四个只读寄存器 ":、"\.、"% 和 "\#
	6. 表达式寄存器 "=
	7. 选择和拖放寄存器 "\*、"+ 和 "~
	8. 黑洞寄存器寄存器 "\_
	9. 最近搜索模式寄存器 "/
- %寄存器中存储了当前文件的文件名
- \#包含当前文件的目录路径

####录制宏命令
- 用*q< register>*\(regeister是指用户自己定义的从a-z的寄存器\)，然后进行你要重复的操作，可以使很多步操作哦，完成 后用 *q* 来结束。这样，当你需要重新做这些操作的时候，只需要用*n@< register>*来调用即可,n为执行次数，省略为1  
*@@* 重复上一个操作

####修改文件名
- *:saveas filename* 改变当前文件名立即保存
- *:file filename* 改变当前文件名暂时不保存

####折叠
- *zf*  F-old creation (创建折叠)    命令：zf 行数 j 
- *zo*  O-pen a fold (打开折叠)  *zO* 打开全部 
- *zc*  C-lose a fold (关闭折叠)  *zC* 关闭全部
- *zA* 
你可以重复 "zr" 和 "zm" 来打开和关闭若干层嵌套的折叠

####键盘映射（@TODO）
- *:map ,*           : 列出以逗号开始的键盘映射
- *\<unique\>* 如果该映射已经存在，系统会提示错误

####编辑技巧
- 普通模式
	- *di\[* 删除一对 \[\] 中的所有字符
	- *di\(* 删除一对 \(\) 中的所有字符
	- *di<* 删除一对 <> 中的所有字符
	- *di\{* 删除一对 \{\} 中的所有字符
	- *dit* 删除一对 HTML/XML 的标签内部的所有字符
	- *di”* di’ 删除一对引号字符 (” 或 ‘ ) 中所有字符
- 插入模式
	- *ci[* 删除一对 \[\] 中的所有字符并进入插入模式
	- *ci(* 删除一对 () 中的所有字符并进入插入模式
	- *ci<* 删除一对 <> 中的所有字符并进入插入模式
	- *ci{* 删除一对 {} 中的所有字符并进入插入模式
	- *cit* 删除一对 HTML/XML 的标签内部的所有字符并进入插入模式
	- *ci”* ci’ 删除一对引号字符 (” 或 ‘) 中所有字符并进入插入模式
- 选择模式
	- *vi[* 选择一对 \[\] 中的所有字符
	- *vi(* 选择一对 () 中的所有字符
	- *vi<* 选择一对 <> 中的所有字符
	- *vi{* 选择一对 {} 中的所有字符

- *dt(* 删除到下一个"("前为之  t( 代表跳转到下一个(前 
- *:set a* 列出配置项a, *:set all* 列出所有配置项
- *ddp* 上下两行调换

####文件编码和格式
- 三个配置文件编码的参数encoding(enc)、fileencoding(fenc)、fileecodings(fencs)
    - enc，vim用于显示的编码，不管最后的文件是什么编码的，vim都会将其转换为当前系统编码来进行处理
    - fencs,是用来在打开文件的时候进行解码的猜测列表
    - fenc，是当前文件的编码，也就是说，一个在vim里面已经正确显示了的文件(前提是你的系统环境跟你的enc设置匹配)，你可以通过改变 fenc后再w来将此文件存成不同的编码
- fileformats(ffs)指定优先处理的文件格式，fileformat(ff)指定当前文件的格式
- 改变文件格式（dos->unix）方法如下: 
        
        vim dos.txt
        :set fileformat=unix
        :w 
       
>[VIM乱码原因与解决方案](http://blog.csdn.net/keepliving/article/details/5623362)

####单词间移动
- *w*、*e*向后移动一个单词（分别停留在词首和词尾），*b*向后移动一个单词（停留在词尾）
- 单词定义通过*iskeyword*进行设置，具体参见*：h iskeyword*
- **WORD**（由非空白字符序列组成字符串，以空白分隔，空行也算一个WORD）移动，*W*、*E*、*B*移动含义和w、e、b相同，只是移动幅度从一个单词变为一个WORD

####个性化vimrc

	set autoindent
自动缩排，如当前行是从第3个字符的位置开始编辑的,按回车后光标会自动定位在下一行第三3个字符的位置。

	set paste
置粘贴模式，这样粘贴过来的程序代码就不会错位了。

	set guifont=* 显示字体对话框设置字体
	set guifontwide=*
wide是双字节字体，这样可以分别设置中文和英文字体

####撤销undo
- `set undolevels=5000` 设置可撤销的次数
- `u` 撤销命令，`:redo` <C-R> 为取消撤销（重做）
- `:undolist` 显示撤销列表，`:undo+编号`撤销到某个分支
- `g-`,`g+` 返回较早的文本状态和返回较新的文本状态
- `:earlier 10m` 恢复到十分钟前的文本状态，`:later 5s`跳转到5秒钟后的状态

####其他
把当前文件转换成HTML文件  

	:runtime! syntax/2html.vim

---

##程序员常用技巧

- % 跳到匹配的括号,跳到匹配处，比如括号之间，C的宏指令#if #else #endif之间
- gD 跳到局部变量的定义处，高亮所有局部变量  <C-O>跳转回来,<C-I>结合<C-O>可以来回跳转
- [I     : 显示光标处的狭义字可以匹配的行(高级指令)  
	可以全文查找与光标处的狭义字相匹配的字，  
	这在查找函数原型和实现，或者变量使用的时候很有用
- **排版** 在任何处v%选中该括号内的所有内容，然后=可以按C语言排版程序  
gg=G可以全文排版
- **缩进** 选中代码块然后\>或者\<可以改变代码块的缩进 
　*>>* 和 *<<* 改变一行的缩进
- 给代码插入行号

		:g/^/exec "s/^/".strpart(line(".")."    ", 0, 4)

####配色
- 配色文件在colors目录下
- colorscheme murphy(配色方案名称)  
- 其他配色方案可以参考：<http://code.google.com/p/vimcolorschemetest/>  
可以在其中找到一个自己喜欢的。安装colorscheme时，只需要把它们拷贝到.vim/color目录下就行了。
- 【插件】 ***csExplorer***  
使用输入:ColorSchemeExplorer即可

>[自己动手扩展vim插件——配色篇](http://blog.csdn.net/mdl13412/article/details/8129904)

####自动补全 

- *<C\-P>和<C\-N>* 连续按选择
-【插件】***AutoClose*** --（http://www.vim.org/scripts/script.php?script_id=1849 ）
不过这个插件目前我在使用的过程中发现有个缺陷，就是在嵌套的括号中再插入一组括号，右括号插入不了，只能采取关闭插件功能，或者采用粘贴的方式。例如：
        if ( ( a  >  b  &&  c  >  d )
你要在“b”后面插一个右括号，你会发现无法完成操作。当你insert模式下输入“）”时，光标直接跳到“d”后面的括号“）”之后，这种情况下 我解决这个问题的办法是关闭插件，输入“/a” AutoClose Off，然后插入右括号;再打开插件功能,输入“/a” AutoClose On。
- 【插件】***neocomplcache*** 和***neosnippet*** @TODO
>[neocomplcache和neosnippet配置心得](http://yunying.me/?p=486)
>[打造一个有感觉的Vim（二）](http://www.cnblogs.com/iiaijimaai/archive/2013/05/19/3054115.html)

- 【插件】***snipMate***
	- 通过tab键触发  
	- 在snippets目录下配置代码片段  
	- \_.snippets文件是全局配置

####注释开关
- **EnhancedCommentify** -- 程序代码注释 （<http://www.vim.org/scripts/script.php?script_id=23>） 
	-	*\<leader\>x* 实现注释的开闭
	-	*\<leader\>c* 开闭注释然后跳转到下一行
	要实现上面的注释自动缩进、在/×  ×/填充空格，需要定义两个全局变量来控制脚本的执行.你可以在.vimrc中进行定义，以控制制缩进、注释样式等来符合你的要求。详细变量也参脚本说明。 

			1         let  g:EnhCommentifyRespectIndent= 'Yes'
			2         let  g:EnhCommentifyPretty= 'Yes'

	不支持esqlc，下载插件后需要手动添加对esqlc的支持

- **NerdComment** 更加强大的注释插件
	- *<\leader\>ci* 加注释，再按取消注释
	- *\<leader\>cc* 加注释，再按重复添加
	- *\<leader\>cu* 取消注释
	- *\<leader\>cA* 行尾注释
	- `let NERDSpaceDelims = 1` 在左注释符之后，右注释符之前留有空格

####代码比较
- `diffsplit file2` 水平分割窗口与当前文件比较，
- `vert diffsplit file2` 垂直分割窗口与当前文件比较
- `:set diffopt=context:3` 显示不同文本的上下文3行，默认为6行
- `:diffupdate` 强制更新比较结果
- *[c*、*]c* 查找前（后）一个不同点
- 文件合并： `dp`(diff put),`do`(diff get)

####网络编辑
 【插件】***netrw***（vim7已自带此插件）：  
    
	:e ftp://user@host:port/filepath
阅读目录命令最后要加斜杠，目录浏览方式通过i改变,s改变排序方式

####代码模板
【插件】***load_template***
>[《vimer.cn原创vim(gvim)插件load_template正式发布》](http://www.vimer.cn/2010/02/vimer-cn%E5%8E%9F%E5%88%9Bvimgvim%E6%8F%92%E4%BB%B6load_template%E6%AD%A3%E5%BC%8F%E5%8F%91%E5%B8%83.html)  
snipMate适合较短的片段，load_template适合较大的代码片段

####版本控制(@TODO)

---

##vimscript
*:help vim-script-intro* vimScript的帮助(教程)

>不错的参考文章（共五个部分）: [使用脚本编写 Vim 编辑器\[1\]](http://www.ibm.com/developerworks/cn/linux/l-vim-script-1/) [\[2\]](http://www.ibm.com/developerworks/cn/linux/l-vim-script-2/) [\[3\]](http://www.ibm.com/developerworks/cn/linux/l-vim-script-3/) [\[4\]](http://www.ibm.com/developerworks/cn/linux/l-vim-script-4/) [\[5\]](http://www.ibm.com/developerworks/cn/linux/l-vim-script-5/)  

执行脚本命令： *source 脚本地址* 
或者，可以在 Vim 命令行中，在冒号后面直接输入脚本命令。例如：

	：call MyBackupFunc(expand('%'), { 'all':1, 'save':'recent'})

通过在 Vim 内输入 `:help keycodes` 可以看到这些特殊符号的完整列表。 	
学习内置函数 `:help functions`	
内置函数列表 `:help function-list`

---

##关于插件
####使用Bundle管理插件
- 安装Bundle插件,需要安装git支持，然后执行如下命令，后面的目标地址可以自行指定

		git clone https://github.com/gmarik/vundle.git ~/.vim/vimfiles/bundle/vundle
- 修改vimrc文件，添加如下内容
```
set nocompatible               " be iMproved
filetype off                   " required!
 
set rtp+=~/.vim/bundle/vundle/  "需要修改该路径到安装目录
call vundle#rc()
 
" let Vundle manage Vundle
" required!
Bundle 'gmarik/vundle'
" original repos on github
Bundle 'tpope/vim-fugitive'
Bundle 'Lokaltog/vim-easymotion'
Bundle 'rstacruz/sparkup', {'rtp': 'vim/'}
Bundle 'tpope/vim-rails.git'
" vim-scripts 上的插件可以直接配置名字 
Bundle 'L9'
Bundle 'FuzzyFinder'
" non github repos
Bundle 'git://git.wincent.com/command-t.git'
" ...
 
filetype plugin indent on     " required!
"
" Brief help  -- 此处后面都是vundle的使用命令
" :BundleList          - list configured bundles
" :BundleInstall(!)    - install(update) bundles
" :BundleSearch(!) foo - search(or refresh cache first) for foo
" :BundleClean(!)      - confirm(or auto-approve) removal of unused bundles
"
" see :h vundle for more details or wiki for FAQ
" NOTE: comments after Bundle command are not allowed.		
```
- 默认会将插件安装到.vim目录下，需要修改`bundle/vundle/autoload/vundle.vim`中的`vundle#rc`函数（43行），将路径改成需要下载到的目标地址即可
- Bundle 命令介绍
	- **BundleSearch** keyword  搜索关键字为keyword的插件
	- **BundleInstall** 安装插件，已安装过的会自动跳过
	- **BundleUpdate** 更新所有插件，一旦git源中插件的内容有变化会自动更新
	- **BundleClean**  将vimrc配置中的`Bundel XXX`注释，然后执行该命令，XXX插件会被删除
	- **BundleList** 列出所有已启用的插件

####其他
- *:set runtimepath* 查看插件安装路径，vim插件一般安装在 5 个地方,可以通过`:set rtp+=xxx`修改
- *:scriptnames* 列出所有执行过的脚本名字，以它们初次执行之顺序排列。（**注意：按顺序加载**）  
**TIPS:** ~\vimfiles下便于迁移和版本升级,使用网盘同步可以让用户体验一致

- ***vimperator*** 像使用vim一样使用firefox的插件  

- macvim中文输入法执行时被错误捕获的问题：  
执行:```defaults write org.vim.MacVim MMUseInlineIm 0```

---

##参考
>[闲耘的Vim](http://wiki.hotoo.me/Vim.html) Vim非常全面的介绍。  
>[波斯克斯](http://www.berlinix.com/index.php) 关于不错的涉及vim尤其是vimViki的网络日志
>[VIM学习笔记](http://www.360doc.com/content/10/1128/15/4807202_73143894.shtml) 很不错的学习笔记，图文并茂



###修订记录：
- *201204*   初稿
- *20120607* 增加rnu
- *20140127* 增加了文件比较，编码格式，单词间移动，撤销
- *20140201* 增加Bundle管理插件
- *20150515* 新增了macvim中文输入法冲突的问题 
