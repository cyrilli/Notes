---
title: PyQt (3)
date: 2016-05-19 21:48:05
tags: -PyQt -Python -GUI
categories: GUI
---
# PyQt Tutorial 3: QTimer
## Example 1:

		import sys
		from PyQt4.QtGui import *
		from PyQt4.QtCore import *
		 
		app = QApplication(sys.argv)
		label = QLabel("<font color=red size=128><b>Hello PyQT!</b></font>")
		label.setWindowFlags(Qt.SplashScreen)
		label.show()
		QTimer.singleShot(10000, app.quit) # 设置10s后自动退出
		app.exec_()

In this example, a windown which prints “Hello PyQT!” will appear in the screen, and then it will terminate in 10 seconds.  
  
## Example 2:
		# 初始化一个定时器
		self.timer = QTimer(self)
		# 在定时器计时结束时触发self.showNum
		self.timer.timeout.connect(self.showNum)
		# 每1000毫秒计时一次
		self.timer.start(1000)
		
		def showNum(self):
			count = count + 1
			print(count)
  
## A trick to use QTimer with Try and Finally:
In the example above, self.showNum is called every 1 second, and because self.showNum only takes very little time to run, we don't need to worry about overlapping calls. But if the slot we call takes longer time than the time we have set to rerun the slot, there will be overlapping calls. To deal with this we can use Try and Finally as shown below.

    def start(self):
        self.video = Video(cv2.VideoCapture(0))
        self._timer = QtCore.QTimer(self)
        try:
            self._timer.timeout.connect(self.play)
        finally:
            self._timer.start(10)
            self.update()

Now the timer will only start couonting 10 ms after `self._timer.timeout.connect(self.play)` is finished.