---
title: PyQt (1)
date: 2016-05-19 10:17:37
tags: -PyQt -Python -GUI
categories: GUI
---
# PyQt Tutorial 1: Menu, Toolbar, and Button
PyQt4 is implemented as a set of Python modules. It has 440 classes and 6000 functions and methods. PyQt4's classes are divided into several modules:  
  
+ QtCore: The QtCore module contains the core non GUI functionality. This module is used for working with time, files and directories, various data types, streams, URLs, mime types, threads or processes.
+ QtGui: The QtGui module contains the graphical components and related classes. These include for example buttons, windows, status bars, toolbars, sliders, bitmaps, colours, and fonts.
+ QtNetwork: The QtNetwork module contains the classes for network programming. These classes facilitate the coding of TCP/IP and UDP clients and servers by making the network programming easier and more portable.
+ QtXml: The QtXml contains classes for working with XML files. This module provides implementation for both SAX and DOM APIs.
+ QtSvg: The QtSvg module provides classes for displaying the contents of SVG files. Scalable Vector Graphics (SVG) is a language for describing two-dimensional graphics and graphical applications in XML.
+ QtOpenGL: The QtOpenGL module is used for rendering 3D and 2D graphics using the OpenGL library. The module enables seamless integration of the Qt GUI library and the OpenGL library.
+ QtSql: The QtSql module provides classes for working with databases.  
  
## A Simple Example  
		#!/usr/bin/python
		# -*- coding: utf-8 -*-

		import sys
		from PyQt4 import QtGui, QtCore
		#定义一个继承自QtGui.QMainWindow类的Example类
		class Example(QtGui.QMainWindow):
		    def __init__(self):
		        super(Example, self).__init__()
				#以下为四个自定义的函数：
				#设置窗口大小位置，窗口标题和图标
		        self.initUI()
				#创建窗口中的Button
		        self.defineButton()
				#创建窗口中的Menu
		        self.defineMenu()
				#创建窗口中的Toolbar
		        self.defineToolbar()

		        self.show()
		
		    def initUI(self):
		        self.setGeometry(300, 300, 400, 400)
		        self.setWindowTitle('Icon')
		        self.setWindowIcon(QtGui.QIcon('icon.png'))
		
		    def defineButton(self):
		        button = QtGui.QPushButton("Quit", self)
				#将定义好的Button与所要执行的程序相连（signal and slot）
		        button.clicked.connect(QtGui.qApp.quit)
				#使用推荐的Button大小，设置Button位置
		        button.resize(button.sizeHint())
		        button.move(100, 100)
		
		    def defineMenu(self):
		
		    	#定义一个动作及其各种属性（快捷键，状态提示，动作触发的程序）
		        exitAction = QtGui.QAction('&Exit', self)
		        exitAction.setShortcut('Ctrl+Q')
		        exitAction.setStatusTip('Exit application')
		        exitAction.triggered.connect(QtGui.qApp.quit)
				
		        self.statusBar()
		        menubar = self.menuBar()
		        fileMenu = menubar.addMenu('&File')
		        fileMenu.addAction(exitAction)
		
		
		    def defineToolbar(self):
				#定义一个动作
		        exitAction = QtGui.QAction('&Exit', self)
		        exitAction.setShortcut('Ctrl+Q')
		        exitAction.setStatusTip('Exit application')
		        exitAction.triggered.connect(QtGui.qApp.quit)

		        self.toolBar = self.addToolBar("Extraction")
		        self.toolBar.addAction(exitAction)
		
		
		def main():
		    app = QtGui.QApplication(sys.argv)
		    ex = Example()
		    sys.exit(app.exec_())
		
		
		if __name__ == '__main__':
		    main()

When runnuing this example, we should see a window like this:  
![SimplExample](http://cl.ly/2x3G3N3Q2I2A/SimpleExample.png)

In this example, all the actions I used are `QtGui.qApp.quit` because I am lazy, but we can definely use self defined methods here.