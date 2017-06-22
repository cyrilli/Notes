---
title: PyQt (2)
date: 2016-05-19 20:07:04
tags: -PyQt -Python -GUI
categories: GUI
---
# PyQt Tutorial 2: Layout Management
## Absolute positioning
The programmer specifies the position and the size of each widget in pixels. In the previous tutorial, I used absolute positioning to decide the position of the button.  
We use the move() method to position our widgets. We position them by providing the x and y coordinates. The beginning of the coordinate system is at the left top corner. The x values grow from left to right. The y values grow from top to bottom.  

		lbl1 = QtGui.QLabel('Zetcode', self)
		lbl1.move(15, 10)  
## Layout classes
### Box layout
To create box layout, we use `QtGui.QHBoxLayout` and `QtGui.QVBoxLayout` class. An example code is shown below:

		#!/usr/bin/python
		# -*- coding: utf-8 -*-
		
		import sys
		from PyQt4 import QtGui
		
		class Example(QtGui.QWidget):
		    
		    def __init__(self):
		        super(Example, self).__init__()
		        
		        self.initUI()
		        
		    def initUI(self):
		        # 创建两个按钮
		        okButton = QtGui.QPushButton("OK")
		        cancelButton = QtGui.QPushButton("Cancel")
				# 创建一个水平的Box布局
		        hbox = QtGui.QHBoxLayout()
				# 将一个stretchable space和两个按钮添加进水平布局中
				# addStretch的作用是把两个按钮挤到右侧
		        hbox.addStretch(1)
		        hbox.addWidget(okButton)
		        hbox.addWidget(cancelButton)

				# 创建一个垂直的Box布局，并把刚才的水平布局放置进来
				# 在水平布局上方添加的stretchable space，会使它靠下方
		        vbox = QtGui.QVBoxLayout()
		        vbox.addStretch(1)
		        vbox.addLayout(hbox)
		        
		        self.setLayout(vbox)    
		        
		        self.setGeometry(300, 300, 300, 150)
		        self.setWindowTitle('Buttons')    
		        self.show()
		        
		def main():
		    
		    app = QtGui.QApplication(sys.argv)
		    ex = Example()
		    sys.exit(app.exec_())
		
		
		if __name__ == '__main__':
		    main()  
When runing the code, we should see a window like this:  
![BoxLayout](http://cl.ly/1x29053t2v04/BoxLayout.png)  
### Grid Layout  
The most universal layout class is the grid layout. This layout divides the space into rows and columns. To create a grid layout, we use the `QtGui.QGridLayout` class.  
		# 创建QtGui.QGridLayout类的一个实例grid
		grid = QtGui.QGridLayout()
		# 设置为application window的layout
        self.setLayout(grid)
 
        names = ['Cls', 'Bck', '', 'Close',
                 '7', '8', '9', '/',
                '4', '5', '6', '*',
                 '1', '2', '3', '-',
                '0', '.', '=', '+']
        
        positions = [(i,j) for i in range(5) for j in range(4)]
        
        for position, name in zip(positions, names):
            
            if name == '':
                continue
            # 用每个名字定义一个button
			button = QtGui.QPushButton(name)
			# 将每个button加入到grid layout中
            grid.addWidget(button, *position)  
We can also set widget to span multiple columns or rows in a grid.  

		grid.addWidget(authorEdit, 2, 1)		#放置在第二行第一列的位置
		grid.addWidget(reviewEdit, 3, 1, 5, 1)  #跨越第三行第一列到第五行第一列的位置
