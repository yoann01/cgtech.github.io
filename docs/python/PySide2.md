# Using .qrc Files (pyside2-rcc)


!!!note
    The Qt Resource System is a mechanism for storing binary files in an application.
    The most common uses are for custom images, icons, fonts, among others.

>- The .qrc file
Before running any command, add information about the resources to a .qrc file. 
In the following example, notice how the resources are listed in icons.qrc

```c
</ui>
<!DOCTYPE RCC><RCC version="1.0">
<qresource>
    <file>icons/play.png</file>
    <file>icons/pause.png</file>
    <file>icons/stop.png</file>
    <file>icons/previous.png</file>
    <file>icons/forward.png</file>
</qresource>
</RCC>

```

>- Generating a Python file

Now that the icons.qrc file is ready, use the pyside2-rcc tool to generate a Python class containing the binary information about the resources

```sh
pyside2-rcc icons.rc -o rc_icons.py
```


```py
from PySide2.QtGui import QIcon, QKeySequence, QPixmap
playIcon = QIcon(QPixmap(":/icons/play.png"))
previousIcon = QIcon(QPixmap(":/icons/previous.png"))
pauseIcon = QIcon(QPixmap(":/icons/pause.png"))
nextIcon = QIcon(QPixmap(":/icons/forward.png"))
stopIcon = QIcon(QPixmap(":/icons/stop.png"))

```

# Using .ui file

We've created a very simple UI. The next step is to get this into Python and use it to construct a working application.

>- Loading the .ui file directly

To load .ui files in PySide we first create a QUiLoader instance and then call the loader.load() method to load the UI file.

```py
import sys
from PySide2 import QtCore, QtGui, QtWidgets
from PySide2.QtUiTools import QUiLoader

loader = QUiLoader()
app = QtWidgets.QApplication(sys.argv)
window = loader.load("mainwindow.ui", None)
window.show()
app.exec_()
```

!!!warning
    but slot-signal bindings, which are set in the designer in *.ui file, are not working anyway.


So, for full-function use of designer GUI and slot-signal bindings, the only way I found is to compile *.ui file to python module with pyside UI compiler:


>- Converting your .ui file to Python
Instead of importing your .uic files into your application directly, you can instead convert them into Python code and then import them like any other module. To generate a Python output file run pyside2-uic from the command line, passing the .ui file and the target file for output, with a -o parameter. The following will generate a Python file named MainWindow.py which contains our created UI.

```sh
pyside2-uic mainwindow.ui -o MainWindow.py
```

```py
import sys
from PySide2 import QtWidgets

from MainWindow import Ui_MainWindow


class MainWindow(QtWidgets.QMainWindow, Ui_MainWindow):
    def __init__(self):
        super(MainWindow, self).__init__()
        self.setupUi(self)


app = QtWidgets.QApplication(sys.argv)

window = MainWindow()
window.show()
app.exec_()
```