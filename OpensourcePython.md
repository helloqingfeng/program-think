<h1>Python 开源项目及示例代码</h1>

本页面是俺收集的各种 Python 资源，不定期更新。

下面列出的各种 Python 库/模块/工具，如果名称带超链接，说明是第三方的；否则是 Python 语言内置的。



&lt;hr&gt;







&lt;hr&gt;




&lt;hr&gt;



# 1 算法 #

## 1.1 字符串处理 ##

#### re ####

正则表达式的标准库。

#### StringIO / cStringIO ####

以读写文件的方式来操作字符串（有点类似于内存文件）。

cStringIO 是 C 语言实现的，提供高性能；而 StringIO 是 Python 实现的，提供 Unicode 兼容性。

#### [chardet](https://github.com/erikrose/chardet) ####

chardet 可以猜测任意一段文本的字符集编码。对于编码类型未知的文本，它会很有用。

chardet 既可以作为模块来使用，也可以作为命令行工具来使用。

代码示例
```
import chardet
print chardet.detect(bytes) 
```

## 1.2 数学类 ##

#### math ####

这个标准库顾名思义，封装了常用的数学函数（开方、指数、对数、三角函数、等）

#### random ####

这个标准库顾名思义，是用来进行随机数生成的

代码示例
```
# 生成 0-100 的随机数
import random
random.seed()
random.randint(0, 100)
```

#### fractions ####

这个标准库封装了跟有理数（分数）相关的运算


## 1.3 安全类 ##

#### hashlib ####

在 Python 2.5 版本加入到标准库中。通过它，你可以很方便地计算各种散列值。

它支持的哈希算法有：MD5 SHA1 SHA224 SHA256 SHA384 SHA512

关于散列算法，俺写过一篇扫盲（在[这里](http://program-think.blogspot.com/2013/02/file-integrity-check.html)）。

代码示例
```
# 计算字符串的 SHA1 散列值
import hashlib
sha1 = hashlib.sha1('Hello world').hexdigest()
```

#### [PyCrypto](http://www.dlitz.net/software/pycrypto/) ####

这个库包含了常见的对称加密算法（DES、AES、IDEA、等）、公钥加密算法（RSA、DSA、等）、散列算法（MD5、SHA1、RIPEMD、等）。

#### [pyOpenSSL](http://pyopenssl.sourceforge.net/) ####

OpenSSL 在加密领域可是大名鼎鼎。这个库使用 Python 对 OpenSSL 进行很薄的封装。




&lt;hr&gt;




# 2 跨编程语言 #

Python 可以很容易地跟其它编程语言整合。整合之后，就可以在 Python 代码中使用其它编程语言的函数、模块、库，非常爽！

## 2.1 整合 C / C++ 语言 ##

#### ctypes ####

ctypes 在 Python 2.5 版本加入到标准库中。

通过它，你可以很方便地调用 C/C++ 动态库导出的函数，可以在 Python 中使用各种 C/C++ 的数据类型（比如指针）。

代码示例
```
# 调用 Linux/Unix 系统的标准 C 函数，获取当前时间
from ctypes import *
libc = CDLL('libc.so.6')
time = libc.time(None)

# 调用 Windows 系统 API，弹出消息提示框
from ctypes import c_int, WINFUNCTYPE, windll
from ctypes.wintypes import HWND, LPCSTR, UINT
prototype = WINFUNCTYPE(c_int, HWND, LPCSTR, LPCSTR, UINT)
paramflags = (1, 'hwnd', 0), (1, 'text', 'Hi'), (1, 'caption', None), (1, 'flags', 0)
MessageBox = prototype(('MessageBoxA', windll.user32), paramflags)
MessageBox(text='Hello world'，flags=2)
```

#### [SWIG](http://swig.org/) ####

这是一个很老牌的、有名气的工具，它可以把多种语言（Java、Python、C#、Ruby、PHP、Perl、Lua、Go、等）整合到 C/C++ 中。

#### [Cython](http://cython.org/) ####

这个工具可以让你用 Python 的语法写扩展模块的代码，然后它帮你把 Python 代码编译为本地动态库（机器码）。

用它编译出来的扩展模块，其性能跟 C/C++ 编写的扩展模块相当。

## 2.2 整合 JVM 平台 ##

#### [Jython](http://www.jython.org/) ####

通过 Jython 可以让 Python 代码运行在 JVM 上，并且可以调用其它的 JVM 语言的代码（比如 Java Scale）

## 2.3 整合 dotNet 平台 ##

#### [IronPython](http://ironpython.net/) ####

通过 IronPython 可以让 Python 代码运行在 dotNET 平台上，并且可以调用其它的 dotNET 语言的代码（比如 C# F#）

## 2.4 整合 Objective-C 语言 ##

#### [PyObjC](http://pyobjc.sourceforge.net/) ####

这是用 Python 封装 Mac OS X 上的 Objective-C 库。




&lt;hr&gt;




# 3 操作系统相关 #

#### os ####

这是一个非常基本的标准库，提供了常见的操作系统相关操作。

## 3.1 文件和目录操作 ##

#### shutil ####

相对于 os 标准库，shutil 标准库提供了一些比较高级的文件和目录操作（目录递归复制、目录递归删除、目录压缩打包、等）

代码示例
```
# 递归删除某个目录
import shutil
shutil.rmtree(xxxx)
```

#### glob ####

这个标准库用于查找文件（支持通配符）

代码示例
```
# 获取当前目录所有 txt 文件
import glob
files = glob.glob('./*.txt')
```

#### fnmatch ####

这个标准库用于匹配文件名（支持通配符）

代码示例
```
# 列出当前目录所有 txt 文件
import os, fnmatch
for file in os.listdir('.') :
    if fnmatch.fnmatch(file, '*.txt') :
        print(file)
```

#### tempfile ####

使用这个标准库，可以安全地生成临时文件或临时目录。

## 3.2 本地进程间通信（IPC） ##

#### subprocess / multiprocessing ####

用于进程管理的标准库，可以启动子进程，通过标准输入输出跟子进程交互。

其中 multiprocessing 是 2.6 版本加入到标准库的。

#### signal ####

用于进程信号处理的标准库。

#### mmap ####

提供了内存映射文件的支持。

代码示例
```
# 利用 mmap 在父子进程间交换数据
import os
import mmap

map = mmap.mmap(-1, 13)
map.write("Hello world")

pid = os.fork()

if pid == 0: # 子进程
    map.seek(0)
    print map.readline()
    map.close()
```

## 3.3 Windows 系统相关 ##

#### [PyWin32](http://python.net/crew/mhammond/win32/) ####

这个第三方库封装了 Windows API 及 COM API。通过它可以方便地用 Python 进行 Windows 编程（调用 COM 组件、编写 Windows 服务、等）。

## 3.4 Linux / Unix 系统相关 ##

#### syslog ####

通过这个标准库，可以很方便地跟 POSIX 的 syslog 服务进行交互。

## 3.5 程序打包 ##

#### [PyInstaller](http://www.pyinstaller.org/) ####

PyInstaller 可以把你的 Python 代码制作成独立运行的程序（不依赖 Python 环境就可以运行）。

该工具支持多种操作系统，包括：Windows、Linux、Mac OS X、Solaris、AIX、等。

#### [py2exe](http://www.py2exe.org/) ####

py2exe 的功能类似 PyInstaller，但只支持 Windows 平台。

#### [py2app](https://bitbucket.org/ronaldoussoren/py2app) ####

它很类似于 [py2exe](http://www.py2exe.org/)，差别在于 [py2exe](http://www.py2exe.org/) 支持 Windows 平台，而 [py2app](https://bitbucket.org/ronaldoussoren/py2app) 支持 Mac OS X 平台。

#### [EasyInstall / Setuptools](https://pypi.python.org/pypi/setuptools) ####

这套工具可以帮助你进行第三方库的管理（下载、编译、安装、升级、卸载）




&lt;hr&gt;




# 4 Web 开发 #

如今 Web 开发很火，俺把 Web 相关的单独分一类。

## 4.1 HTTP 协议 ##

#### httplib / httplib2 / http.request / urllib.parse ####

这几个库可以进行各种 HTTP 客户端请求（GET、POST、等）。

Python2 的模块名叫 httplib / httplib2，到 Python3 模块名改为 http.request / urllib.parse

代码示例
```
# 读取指定 URL 的网页内容
import urllib
handle = urllib.urlopen('http://www.google.com')
page = handle.read()
handle.close()
```

## 4.2 Web Server ##

#### SimpleHTTPServer / http.server ####

提供轻量级 HTTP Server 的标准库。

Python2 的模块名叫 SimpleHTTPServer，到 Python3 模块名改为 http.server

代码示例
```
#一个极简单的 HTTP 服务
import SocketServer
import SimpleHTTPServer

PORT = 8000
Handler = SimpleHTTPServer.SimpleHTTPRequestHandler
httpd = SocketServer.TCPServer(('', PORT), Handler)
print 'serving at port', PORT
httpd.serve_forever()
```

## 4.3 Web 开发框架 ##

#### [Django](http://www.djangoproject.com/) ####

在 Python 社区，Django 是目前最有影响力的 Web 开发框架。该框架很重型，内置了 Web 服务端开发常用的组件。

Django 应用范围很广，比如 Google 的 Web 开发平台 GAE 就支持它。

Django 完全支持前面提到的 Jython 运行环境，可以运行在任何 J2EE 服务器上。

#### [TurboGears](http://www.turbogears.org/) ####

又一个重型的 Web 开发框架，名气仅次于 Django。

#### [Tornado](http://www.tornadoweb.org/) ####

这是 FriendFeed 开发的 Web 框架。FriendFeed 被 Facebook 收购之后，该框架被开源。

#### [Flask](http://flask.pocoo.org/) ####

这是一个很轻量级的 Web 框架，但是扩展性很好。

代码示例
```
# 用 Flask 写 Hello world
from flask import Flask
app = Flask(__name__)
 
@app.route("/")
def hello():
    return "Hello World!"
 
if __name__ == "__main__":
    app.run()
```

## 4.4 Web前端 / JS整合 ##

#### [Pyjamas / pyjs](http://pyjs.org/) ####

这是从 GWT（Google Web Toolkit）移植的第三方库。提供了 Python 到 JS 的编译，AJAX 框架等功能。
Pyjamas 甚至能用来开发桌面 GUI 应用。

#### [pyjaco](https://github.com/chrivers/pyjaco) ####

这也是一个 Python 到 JavaScript 的编译工具。

## 4.5 浏览器整合 ##

#### webbrowser ####

操纵当前系统的默认浏览器，访问指定 URL 的页面。

代码示例
```
# 用默认浏览器打开 Google 主页
import webbrowser
webbrowser.open('http://www.google.com')
```

#### [pyv8](https://code.google.com/p/pyv8/) ####

[v8](https://code.google.com/apis/v8/) 是 Google 开发的 JavaScript 解释引擎。这是对 v8 引擎的 Python 封装。

代码示例
```
import PyV8

ctxt1 = PyV8.JSContext()
ctxt1.enter()
ctxt1.eval('1+2')  # 对 JS 表达式求值

class Global(PyV8.JSClass) :  # 定义一个兼容 JS 的类
    def hello(self) :
        print 'Hello world'

ctxt2 = PyV8.JSContext(Global()) # 创建一个 JS 上下文，传入 Global 类的对象
ctxt2.enter()                    
ctxt2.eval('hello()')  # 调用 hello() 函数
```

#### [PyWebKitGtk](https://code.google.com/p/pywebkitgtk/) ####

[WebKitGtk](http://webkitgtk.org/) 是一个基于 WebKit 的 Web 渲染引擎。这是 WebKitGtk 的 Python 封装。




&lt;hr&gt;




# 5 网络编程 #

## 5.1 标准协议 ##

### 5.1.1 链路层 / 网络层 ###

#### [Scapy](http://www.secdev.org/projects/scapy/) ####

这是一个底层的网络库，可以在不同协议层次构造网络数据包（包括链路层、网络层、传输层），还支持 Sniffer 抓包。

搞网络安全的网友应该会喜欢这个库。

代码示例
```
# 传统的 ping 扫描（网络层）
ans,unans = sr(IP(dst='192.168.1.1-254')/ICMP())

# 局域网内的 ARP 扫描（链路层）
ans,unans = srp(Ether(dst='ff:ff:ff:ff:ff:ff')/ARP(pdst='192.168.1.0/24'), timeout=2)
```

### 5.1.2 传输层 ###

#### socket ####

Python 标准库很早就提供了对 socket 编程的支持。

这个标准库是对伯克利套接字进行简单的封装，其 API 基本上跟 BSD SOCKET 一一对应。

#### asyncore ####

这个标准库提供了异步 SOCKET 的支持。

#### asynchat ####

这个标准库基于上述的 asyncore，提供更高层的 API，简化异步通讯编程。

### 5.1.3 应用层 ###

#### ftplib ####

封装 FTP 协议（文件传输）的标准库

#### smtplib ####

封装 SMTP 协议（邮件发送）的标准库

#### imaplib ####

封装 IMAP 协议（邮件接收）的标准库

#### poplib ####

封装 POP3 协议（邮件接收）的标准库

#### [PycURL](http://pycurl.sourceforge.net/) ####

cURL 是一个功能很强的网络库/网络工具，支持 N 多应用层协议。这是用 Python 封装的第三方库。

关于 cURL，俺前几年写过一篇博文推荐它（在[这里](http://program-think.blogspot.com/2009/03/opensource-review-curl-library.html)）。

#### [jabber.py](http://jabberpy.sourceforge.net/) ####

Jabber（又称 XMPP）是IM（即时通信）协议的标准。这是用 Python 封装的第三方库。

#### [irclib](https://bitbucket.org/jaraco/irc) ####

IRC 是 Internet Relay Chat 的缩写。这是用 Python 封装的第三方库。

## 5.2 编码和解码 ##

#### json ####

标准库，提供 JSON 格式的编码和解码。

JSON 格式如今在 Web 开发中广为应用。

代码示例
```
import json

json.dumps(['foo', {'bar': ('baz', None, 1.0, 2)}])
# JSON 编码
# 得到如下字符串
# '["foo", {"bar": ["baz", null, 1.0, 2]}]'

json.loads('["foo", {"bar":["baz", null, 1.0, 2]}]')
# JSON 解码
# 得到如下对象
# [u'foo', {u'bar': [u'baz', None, 1.0, 2]}]
```

#### base64 ####

标准库，提供 Base16、Base32、Base64 格式的编码和解码。

#### binhex ####

标准库，提供 binhex4 格式的编码和解码。

#### uu ####

标准库，提供 uuencode 格式的编码和解码。

#### [Protocol Buffers（protobuf）](https://code.google.com/p/protobuf/) ####

这是 Google 开发的一个跨语言的库，用于网络传输的编码和解码。

它的优点是：跨多种语言、高性能、向前兼容、向后兼容。俺前几年写过一篇博文推荐 protobuf（在[这里](http://program-think.blogspot.com/2009/05/opensource-review-protocol-buffers.html)）。

## 5.3 网络开发框架 ##

#### [Twisted](http://twistedmatrix.com/) ####

这是一个基于 Python 网络通讯开发框架，有十多年历史，名气很大。

它的某些设计类似于 C++ 的 [ACE](http://en.wikipedia.org/wiki/Adaptive_Communication_Environment) 框架。除了能用来进行传输层（TCP UDP）的开发，还提供了若干应用层协议（HTTP、XMPP、SSH、IRC、等）的支持。

代码示例
```
# 实现一个简单的 Echo 服务，监听在 12345 端口
from twisted.internet import protocol, reactor

class Echo(protocol.Protocol) :
    def dataReceived(self, data) :
        self.transport.write(data)

class EchoFactory(protocol.Factory) :
    def buildProtocol(self, addr) :
        return Echo()

reactor.listenTCP(12345, EchoFactory())
reactor.run()
```




&lt;hr&gt;




# 6 数据库 #

为了便于数据库开发，Python 社区制定了数据库的 API 规范（[PEP 249](http://www.python.org/dev/peps/pep-0249/)）。

只要是涉及到数据库操作，标准库和大部分第三方库都会遵循该规范。请看如下几个模块的示例代码。

## 6.1 数据库中间件 ##

### 6.1.1 ODBC ###

#### [pyODBC](https://code.google.com/p/pyodbc/) ####

pyODBC 封装了 ODBC API，通过它可以访问各种数据库（只要有 ODBC 驱动即可）。

代码示例
```
# 查询某个 ODBC 数据源的某个表
import pyodbc
conn = pyodbc.connect('DSN=xxx;PWD=password')
cursor = conn.cursor()
cursor.execute('SELECT field1 FROM table1')
while True :
    row = cursor.fetchone()
    if not row :
        break
    print(row)
cursor.close()
conn.close()
```

#### [ceODBC](http://ceodbc.sourceforge.net/) ####

又一个封装 ODBC API 的第三方库

### 6.1.2 JDBC ###

#### [Jython](http://www.jython.org/) ####

Jython 前面提到过。它可以基于 [JDBC](http://en.wikipedia.org/wiki/Jdbc) 操作数据库。

### 6.1.3 ADO / ADO.NET ###

#### [PyWin32](http://python.net/crew/mhammond/win32/) ####

PyWin32 前面提到过。它可以基于 [ADO](http://en.wikipedia.org/wiki/ActiveX_Data_Objects) 操作数据库。

#### [IronPython](http://ironpython.net/) ####

IronPython 前面提到过。它可以基于 [ADO.NET](http://en.wikipedia.org/wiki/ADO.NET) 操作数据库。


## 6.2 特定数据库 ##

### 6.2.1 MySQL ###

#### [MySQL for Python](http://mysql-python.sourceforge.net/) ####

操作 MySQL 的第三方库。

代码示例
```
# 查询某个 MySQL 数据库的某个表
import MySQLdb
conn = MySQLdb.connect(db='test', passwd='password')
cursor = conn.cursor()
cursor.execute('SELECT field1 FROM table1')
while True :
    row = cursor.fetchone()
    if not row :
        break
    print(row)
cursor.close()
conn.close()
```

### 6.2.2 PostgreSQL ###

#### [psycopg](http://initd.org/psycopg/) ####

操作 PostgreSQL 的第三方库。

#### [psycopg](http://www.pygresql.org/) ####

操作 PostgreSQL 的第三方库。

### 6.2.3 Oracle ###

#### [cx\_Oracle](http://cx-oracle.sourceforge.net/) ####

操作 Oracle 的第三方库。

### 6.2.4 MS SQL Server ###

#### [pymssql](https://code.google.com/p/pymssql/) ####

操作微软 SQL Server 的第三方库。

### 6.2.5 IBM DB2 ###

#### [ibm-db](https://code.google.com/p/ibm-db/) ####

操作 DB2 的第三方库。


### 6.2.6 SQLite ###

#### sqlite3 ####

sqlite3 从 Python 2.5 版本开始加入到标准库中。通过它，你可以很方便地操作 SQLite 数据库。

SQLite 是一个很优秀的轻量级数据库，俺前几年写过一篇博文推荐它（在[这里](http://program-think.blogspot.com/2009/04/how-to-use-sqlite.html)）。

代码示例
```
# 创建一个内存数据库，建表并插入记录
import sqlite3
conn = sqlite3.connect(':memory:')
cursor = conn.cursor()
cursor.execute('CREATE TABLE person (name text, age int)')
cursor.execute('''INSERT INTO stocks VALUES ('TOM',20)''')
conn.commit()
conn.close()
```

### 6.2.7 Berkeley DB ###

#### [PyBSDDB](http://www.jcea.es/programacion/pybsddb.htm) ####

操作 Berkeley DB 的第三方库。

## 6.3 ORM（Object-Relational Mapping） ##

#### [SQLAlchemy](http://www.sqlalchemy.org/) ####

SQLAlchemy 支持的数据库有：MySQL、PostgreSQL、Sqlite、Oracle、MS SQL Server、Firebird、Sybase SQL Server、Informix、等。

代码示例
```
# 通过对象的方式创建两张依赖关系的表
from sqlalchemy import *
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import relation, sessionmaker
 
Base = declarative_base()
 
class Movie(Base) :
    __tablename__ = 'movies'
 
    id = Column(Integer, primary_key=True)
    title = Column(String(255), nullable=False)
    year = Column(Integer)
    directed_by = Column(Integer, ForeignKey('directors.id'))
    director = relation('Director', backref='movies', lazy=False)
 
    def __init__(self, title=None, year=None) :
        self.title = title
        self.year = year

    def __repr__(self) :
        return 'Movie(%r, %r, %r)' % (self.title, self.year, self.director)
 
class Director(Base) :
    __tablename__ = 'directors'
 
    id = Column(Integer, primary_key=True)
    name = Column(String(50), nullable=False, unique=True)
 
    def __init__(self, name=None) :
        self.name = name
 
    def __repr__(self) :
        return 'Director(%r)' % (self.name)
 
Base.metadata.create_all(create_engine('dbms://user:pwd@host/dbname'))
```

#### [SQLObject](http://sqlobject.org/) ####

SQLObject 支持的数据库有：MySQL、PostgreSQL、Sqlite、MS SQL Server、Firebird、Sybase SQL Server、SAP DB、等。

代码示例
```
# 通过对象的方式创建表
from sqlobject import *
sqlhub.processConnection = connectionForURI('sqlite:/:memory:')

class Person(SQLObject) :
    first_name = StringCol()
    last_name = StringCol()

Person.createTable()
```




&lt;hr&gt;




# 7 桌面 GUI 开发 #

## 7.1 GUI 框架 / 组件库 ##

### 7.1.1 基于 Tk ###

[Tk](http://en.wikipedia.org/wiki/Tk_(framework)) 是一个跨平台的界面组件库。

#### Tkinter / tkinter ####

这是 Python 内置的标准库，封装了 Tcl/Tk 界面库。

Python2 的模块名叫 Tkinter，到 Python3 模块名改为 tkinter

代码示例
```
# 用 Tkinter 写 Hello world
from Tkinter import *

if __name__ == '__main__' :
    root = Tk()
    label = Label(root, text='Hello world')
    label.pack()
    root.mainloop()
```

### 7.1.2 基于 wxWidgets ###

[wxWidgets](http://en.wikipedia.org/wiki/WxWidgets) 是 C++ 开发的跨平台框架（不仅包括 GUI，还有其它功能）。

#### [wxPython](http://www.wxpython.org/) ####

在所有的 wxWidgets 的 Python 封装库中，这个是名气最大的。

[Ulipad](https://code.google.com/p/ulipad/)（知名的国产的 Python IDE）就是基于 wxPython 开发的。

代码示例
```
# 用 wxPython 写 Hello world
import wx

class Frame(wx.Frame) :
    pass

class App(wx.App) :
    def OnInit(self) :
        self.frame = Frame(parent=None, title='Hello world')
        self.frame.Show()
        self.SetTopWindow(self.frame)
        return True

if __name__ == '__main__' :
    app = App()
    app.MainLoop()
```

#### [PythonCard](http://pythoncard.sourceforge.net/) ####

又一个基于 wxWidgets 的 GUI 库。

### 7.1.3 基于 GTK+ ###

[GTK+](http://en.wikipedia.org/wiki/GTK%2B) 全称是（GIMP Toolkit），由 C 开发的跨平台界面组件库。

#### [PyGTK](http://www.pygtk.org/) ####

这是 Python 对 GTK 的封装。

代码示例
```
# 用 PyGTK 写 Hello world
import pygtk
pygtk.require('2.0')
import gtk

class HelloWorld :
    def __init__(self) :
        self.window = gtk.Window(gtk.WINDOW_TOPLEVEL)
        self.window.connect('delete_event', self.delete_event)
        self.window.connect('destroy', self.destroy)
        self.window.set_border_width(10)

        self.button = gtk.Button('Hello world')
        self.button.connect('clicked', self.hello, None)
        self.button.connect_object('clicked', gtk.Widget.destroy, self.window)
        self.window.add(self.button)

        self.button.show()
        self.window.show()

    def main(self) :
        gtk.main()

    def hello(self, widget, data=None) :
        print 'Hello world'

    def delete_event(self, widget, event, data=None) :
        print 'delete event occurred'
        return False

    def destroy(self, widget, data=None) :
        gtk.main_quit()

if __name__ == '__main__' :
    hello = HelloWorld()
    hello.main()
```

### 7.1.4 基于 Qt ###

[Qt](http://en.wikipedia.org/wiki/Qt_(toolkit)) 是 C++ 开发的跨平台框架（不仅包括 GUI，还有其它功能）。

#### [PyQt](http://www.riverbankcomputing.com/software/pyqt/) ####

这是 Python 对 Qt 的封装。

代码示例
```
# 用 pyQt 写 Hello world
import sys
from PyQt4.QtGui import *

if __name__ == '__main__' :
    app = QApplication(sys.argv)
    window = QWidget()

    window.resize(320, 240)
    window.setWindowTitle('Hello world')
    window.show()
    sys.exit(app.exec_())
```

#### [PySide](http://www.pyside.org/) ####

这也是 Python 对 Qt 的封装。

### 7.1.5 基于 FLTK ###

[FLTK](http://en.wikipedia.org/wiki/FLTK) 全称是（ Fast Light Tool Kit），由 C++ 开发的跨平台、轻量级界面组件库。

#### [PyFLTK](http://pyfltk.sourceforge.net/) ####

这是 Python 对 FLTK 的封装。

### 7.1.6 基于 Windows 平台 ###

#### [PyWin32](http://python.net/crew/mhammond/win32/) ####

PyWin32 前面提到过。它可以提供原生的 Windows GUI 界面。

#### [IronPython](http://ironpython.net/) ####

IronPython 前面提到过。它可以提供 dotNET 的 GUI 界面。

### 7.1.7 基于 JVM 平台 ###

#### [Jython](http://www.jython.org/) ####

Jython 前面提到过。它可以提供基于 Java 的 [Swing](http://en.wikipedia.org/wiki/Swing_%28Java%29) 界面。

### 7.1.8 其它 ###

#### [EasyGUI](http://easygui.sourceforge.net/) ####

EasyGUI 这是一个很轻量级的库。跟其它 GUI 不同之处在于——没有事件驱动。

#### [PyGUI](http://www.cosc.canterbury.ac.nz/greg.ewing/python_gui/) ####

PyGUI 是一个更高层的 GUI 库，底层分别封装了 [PyWin32](http://python.net/crew/mhammond/win32/)（Windows 平台）、[PyGTK](http://www.pygtk.org/)（Linux 平台）、[PyObjC](http://pyobjc.sourceforge.net/)（Mac OS X 平台）。

#### [Kivy](http://kivy.org/) ####

跨平台的多媒体框架和界面库，用来开发比较炫的界面。

除了支持桌面操作系统，还支持 Android / iOS，支持多点触摸。

#### [OcempGUI](http://ocemp.sourceforge.net/gui.html) ####

基于 PyGame 的一个跨平台 GUI 库。PyGame 下面会提到。

## 7.2 图表/报表 ##

#### [matplotlib](http://matplotlib.org/) ####

这是一个有名的图形库，主要用来绘制数学相关的图形。

跟后面提到的 [SciPy](http://www.scipy.org/) 整合可以起到类似  MATLAB 的效果。效果图在“[这里](http://matplotlib.org/users/screenshots.html)”。

#### [Gnuplot.py](http://gnuplot-py.sourceforge.net/) ####

这是 Python 对 [gnuplot](http://www.gnuplot.info/) 的封装。gnuplot 的效果图在“[这里](http://www.gnuplot.info/screenshots/index.html)”。

#### [PyQtGraph](http://www.pyqtgraph.org/) ####

这是一个纯 Python 的库，依赖于 PyQt4 / PySide。效果图在“[这里](http://www.pyqtgraph.org/images/plotting_sm.png)”。

#### [PyX](http://pyx.sourceforge.net/) ####

这个库可以跟 TeX / LaTeX 无缝整合，支持导出为 PostScript / PDF 格式。适合用来制作报表。效果图在“[这里](http://pyx.sourceforge.net/gallery/index.html)”。

#### [Chaco](http://code.enthought.com/chaco/) ####

这是一个商业公司维护的库，主要提供2维图表。效果图在“[这里](http://docs.enthought.com/chaco/user_manual/annotated_examples.html)”。




&lt;hr&gt;




# 8 处理文件格式 #

## 8.1 处理压缩文件 / 打包文件 ##

### 8.1.1 zip ###

#### zipfile ####

处理 zip 格式的标准库。

### 8.1.2 bzip2（bz2） ###

#### bz2 ####

处理 bzip2 格式的标准库。

### 8.1.3 gzip（gz） ###

#### gzip ####

处理 gzip 格式的标准库。

#### zlib ####

处理 gzip 格式的标准库。

### 8.1.4 tar ###

#### tarfile ####

处理 tar 格式的标准库。

### 8.1.5 7zip（7z） ###

#### [PyLZMA](http://www.joachim-bauch.de/projects/pylzma/) ####

处理 7zip 格式的第三方库。

### 8.1.6 rar ###

#### [rarfile](http://rarfile.berlios.de/) ####

处理 rar 格式的第三方库。

### 8.1.7 msi ###

#### msilib ####

处理 msi 格式的标准库，从 Python 2.5 版本开始提供。

## 8.2 处理标记语言 ##

### 8.2.1 XML ###

#### xml.dom / xml.miniDom / xml.etree.ElementTree ####

用 DOM（Document Object Model）方式处理 XML 文件的标准库。

#### xml.sax / xml.parsers.expat ####

用 SAX（Simple API for XML）方式处理 XML 文件的标准库。

#### [lxml](http://lxml.de/) ####

著名的 C 语言库 libxml 和 libxslt 的 Python 封装。

功能很强，支持 XPath 1.0、XSLT 1.0、扩展 EXSLT、等。还可以用来解析 HTML 格式。

### 8.2.2 HTML ###

#### HTMLParser ####

以回调方式解析 HTML/XHTML 文件内容的标准库。

## 8.3 处理图片 ##

#### [Python Imaging Library (PIL)](http://www.pythonware.com/products/pil/) ####

这是一个很有名气的 Python 图像处理库，支持常见图像文件格式（BMP、JPG、GIF、PNG、等），可以对图像进行各种常见操作（格式转换、旋转、缩放、剪切、等）。

代码示例
```
# 旋转某图片并显示
from PIL import Image
im = Image.open('xxx.jpg')
im = im.rotate(90)
im.show()
```

## 8.4 处理 PDF ##

#### [pyfpdf](https://code.google.com/p/pyfpdf/) ####

这是 [FPDF](http://www.fpdf.org/) 的 Python 移植库，用来生成 PDF 文档。

支持的功能比较全（嵌入字体、嵌入图片），文档也比较详细。

代码示例
```
# 这是个简单 Hello World 示例
from fpdf import FPDF

pdf = FPDF()
pdf.add_page()
pdf.set_font('Arial', 'B', 16)
pdf.cell(40, 10, 'Hello World')
pdf.output('test.pdf', 'F')
```

```
# 支持写入 HTML 语法。目前支持几种常见的 HTML tag
from pyfpdf import FPDF, HTMLMixin

class MyFPDF(FPDF, HTMLMixin) :
    pass
                    
pdf = MyFPDF()
pdf.add_page()
pdf.write_html(html)
pdf.output('test.pdf', 'F')
```

#### [pyPdf](http://pybrary.net/pyPdf/) / [PyPDF2](http://knowah.github.com/PyPDF2/) ####

pyPdf 目前已经不继续升级维护了。PyPDF2 是 pyPdf 的 fork 并继续增加新功能。

除了可以提取文件属性，还可以切分/合并文档，加密/解密文档。

#### [PDFMiner](http://www.unixuser.org/~euske/python/pdfminer/) ####

可以提取 PDF 文件属性以及每页的文本，支持把内容输出为 HTML 格式。


## 8.5 处理 Office 文档 ##

### 8.5.1 Word（doc、docx） ###

#### [PyWin32](http://python.net/crew/mhammond/win32/) ####

PyWin32 前面提到过。它可以基于 [COM](http://en.wikipedia.org/wiki/Component_Object_Model) 操作 Office 文档，包括 Word（本地需要安装 Office）。

### 8.5.2 Excel（xls、xlsx） ###

#### [pyExcelerator](http://sourceforge.net/projects/pyexcelerator/) ####

该库可以支持 Office Excel（97/2000/XP/2003）以及 OpenOffice Calc 的文档。无需依赖外部软件。

#### [PyWin32](http://python.net/crew/mhammond/win32/) ####

PyWin32 前面提到过。它可以基于 [COM](http://en.wikipedia.org/wiki/Component_Object_Model) 操作 Office 文档，包括 Excel（本地需要安装 Office）。

### 8.5.3 Power Point（ppt、pptx） ###

#### [python-pptx](https://github.com/scanny/python-pptx) ####

该库可以用来生成 pptx（Open XML PowerPoint）格式的文档。

#### [PyWin32](http://python.net/crew/mhammond/win32/) ####

PyWin32 前面提到过。它可以基于 [COM](http://en.wikipedia.org/wiki/Component_Object_Model) 操作 Office 文档，包括 Excel（本地需要安装 Office）。

## 8.6 处理 CHM ##

#### [PyCHM](http://gnochm.sourceforge.net/pychm.html) ####

这是基于 [chmlib](http://www.jedrea.com/chmlib/) 的 Python 封装库。可以提取 CHM 文件的属性以及每个页面的内容。

## 8.7 处理 RTF ##

#### [PyRTF](http://pyrtf.sourceforge.net/) ####

这个 Python 库可以用来处理 RTF（富文本格式）文档。




&lt;hr&gt;




# 9 游戏开发 #

#### [PyGame](http://www.pygame.org/) ####

跨平台的 Python 第三方库，用来辅助游戏开发的，名气非常大。

#### [PyOpenGL](http://pyopengl.sourceforge.net/) ####

封装 OpenGL 的 Python 第三方库。

#### [Python-Ogre](http://www.python-ogre.org/) ####

封装 OGRE（3D 渲染引擎）的 Python 第三方库。





&lt;hr&gt;




# 10 数值计算 / 科学计算 #

#### [NumPy](http://www.numpy.org/) ####

NumPy 提供了功能强大、性能很高的数值数组，可以用来进行各种数值计算（包括矩阵运算）。

代码示例
```
# 以下是传统 Python 写法，冗长且速度较慢
a = range(10000000)
b = range(10000000)
c = []
for i in range(len(a)) :
    c.append(a[i] + b[i])

# 以下是 NumPy 的写法，简洁且速度飞快
import numpy as np
a = np.arange(10000000)
b = np.arange(10000000)
c = a + b
```

#### [SciPy](http://www.scipy.org/) ####

SciPy 依赖 NumPy 提供的多维数组。相比 NumPy，SciPy 提供了更高层的数学运算模块（统计、线性代数、积分、常微分方程求解、傅立叶变换、信号处理、等），被广泛用于科研和工程领域。

# 11 其它 #

一些不方便归类的，暂时放到这里。

#### [PyPy](http://www.pypy.org/) ####

这是一个用 Python 写的 Python 解释器（有点绕口令）。

PyPy 支持 JIT（Just-in-time compilation）和沙箱技术，可做到比 CPython 更快的运行速度。