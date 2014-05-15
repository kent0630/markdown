Mac上安装PyQt4环境
============
####环境
- OS10.8.5（64位）
- Python2.7（操作系统自带的python版本）

####1. 下载安装QT5
- 安装 **Xcode Command Line Tools**  
    a.运行Xcode后，找到*Preference*菜单  
    b.在弹出对话框中选择*download*，然后在*Command Line Tools*的一栏点击“install”进行安装    
- 下载网站：<http://qt-project.org/downloads>
- 下载[QT5.2.0 for MAC](http://download.qt-project.org/official_releases/qt/5.2/5.2.0/qt-mac-opensource-5.2.0-clang-offline.dmg)
- 按向导安装即可    

####2. 下载安装SIP
- 下载网站：<http://www.riverbankcomputing.co.uk/software/sip/download>  
- 下载 [sip-4.15.4-snapshot-b4a30e5b9970.tar.gz](http://www.riverbankcomputing.co.uk/static/Downloads/sip4/sip-4.15.4-snapshot-b4a30e5b9970.tar.gz)   
- 执行如下命令编译、安装  
            
        cd sip-4.15.4-snapshot-b4a30e5b9970
    
        python configure.py -d /Library/Python/2.7/site-packages --arch=x86_64  
      
        make  
      
        sudo make install  
  
####3. 下载、运行PyQt
- 下载网站:<http://www.riverbankcomputing.co.uk/software/pyqt/download>

        cd PyQt-mac-gpl-snapshot-4.10.2-ffcf323516fc  
      
        python configure-ng.py -q /Users/xuxiaofeng/Qt5.2.0/5.2.0/clang_64/bin/qmake -d /Library/Python/2.7/site-packages/ --sip /System/Library/Frameworks/Python.framework/Versions/2.7/bin/sip
              
        make
        
        sudo make install

- 运行Demo，如果能正常运行，说明安装成功。
    
        cd PyQt-mac-gpl-4.10.3/examples/demos/qtdemo
    
        python qtdemo.py
        
        
       
       
----
*PyQt4的环境已经搭建完成，接下去是搭建eric4的继承开发环境*           

####4. 下载安装QScintilla2
- 下载网站<http://www.riverbankcomputing.co.uk/software/qscintilla/download>
- 将qt5的bin目录加到环境变量（不然无法执行qmake)

        sudo vi /etc/paths
        添加/Users/xuxiaofeng/Qt5.2.0/5.2.0/clang_64/bin

- 执行如下命令
    
        tar -xvzpf QScintilla-gpl-2.8.tar.gz
        cd QScintilla-gpl-2.8
        cd Qt4Qt5
        qmake qscintilla.pro -spec macx-g++
        make
        sudo make install
        cd ../Python
        python configure.py --sip /System/Library/Frameworks/Python.framework/Versions/2.7/bin/sip
        make
        sudo make install 
        
安装后验证脚本

        import PyQt4.Qsci
        langs = [i for i in dir(PyQt4.Qsci) if i.startswith('QsciLexer')]

        for i,l in enumerate(langs):
    print i,l[9:]

####5. 下载安装Eric4
- 安装Eric4：从 <http://sourceforge.net/projects/eric-ide/files/>下载Eric4最新的版本及i18n

        tar -xvzpf eric4-4.5.18.tar.gz
        tar -xvzpf eric4-i18n-zh_CN.GB2312-4.5.18.tar.gz
        cd eric4-4.4.18
        sudo python install.py
        sudo python install-i18n.py

Eric4 安装在 /Library/Python/2.7/site-packages/eric4 下
到该路径下直接执行 eric4 即可 
   
####问题
1. 如果出现如下报错  
    
        Generating the C++ source for the QtCore module...  
        Error: Unable to create the C++ code.
    
    该问题一般是所用的SIP版本不支持所用的QT版本  
    执行命令`python configure.py -w --confirm-license`判断SIP对QT的版本的支持情况
><http://stackoverflow.com/questions/8664863/installing-pyqt-4-9-on-centos-6-0-fails>

2. QScintilla2安装后，将**Qsci.so**拷贝到`/Library/Python/2.7/site-packages/PyQt4` 安装eric4才不会报错，但是目前运行eric4还是报错，尚未找到原因。



####参考
><http://blog.csdn.net/watsy/article/details/8857252>
><http://i1900.blogbus.com/logs/103861499.html>

####修订记录
- 20140104 初稿
- 20140111 增加eric4的环境搭建

