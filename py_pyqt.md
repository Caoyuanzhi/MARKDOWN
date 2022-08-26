### PyQt入门
***
#### 参考
https://www.wenjiangs.com/doc/5lpaoiqpat
https://zhuanlan.zhihu.com/p/520606210
https://maicss.gitbook.io/pyqt-chinese-tutoral/pyqt6
https://zhuanlan.zhihu.com/p/162866700

***
#### 1.QtWidgets
一个模块，包含了很多用户界面类的模块
#### 2.Qwidget类
所有用户界面类的基类，
#### 3.QApplication
应用类，管理GUI应用程序的控制流和主要设置
1. 初始化：
   ```python
   app = QtWidgets.QApplication(sys.argv)
   ```
2. 退出：
    ```python
    app.exec()
    ```