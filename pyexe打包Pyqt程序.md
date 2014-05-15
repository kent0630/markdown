py2exe打包Pyqt程序
=====
####环境
- Python2.7
- Windows XP SP2

####安装py2exe
- 下载py2exe
- 安装py2exe

####编写
1. 编写脚本setup.py
	
		from distutils.core import setup
		import py2exe

		setup(
	    version = "0.5.0",
	    description = "py2exe sample script",
	    name = "py2exe samples",
	
		# windows = ["simple.py"],
        console = [{"script":"mailtest.py", 
                "icon_resources":[(1, "icon.ico")]}],
		zipfile = None,
		options={"py2exe" : {"compressed": 1,
							 "optimize": 2,
							 "bundle_files": 1, 
							 "includes" : ["sip", "PyQt4._qt"]}}
		)
	
   其中前参数version、description、name、zipfile、compressed、optimize、bundle_files均为可选参数。如果要导出成一个单独的exe文件,bundle_files、zipfile必填。
2. 执行如下命令
		
		python setup.py py2exe --include sip

3. 在dist目录中可找到exe程序

><http://www.cnblogs.com/jans2002/archive/2006/09/30/519393.html>


