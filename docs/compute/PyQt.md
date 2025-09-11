---
title: Concept of PySide6(PyQt)
tags:
  - python
categories: programming
top_img: img/hisameTop.png
---

Using YouTube Video from [freeCodeCamp](https://www.youtube.com/watch?v=Z1N9JzNax2k&t=15000s) as reference

UI creation can be done by `QtWidget` and `QML`, and this post is using **Qt**.

## Requirement

- Python3
- Pyside6
- Qt Designer

## Step 1 - Code understanding

### Level 1

Here is the most basic code to create an empty window of python application with ui

```Python
from PySide6.QtWidgets import QApplication, QWidget

import sys # mean nothing here but important if we need to handle command line argument

app = QApplication(sys.argv)

window = QWidget()
window.show() # calling the window to show because it is hidden in default

app.exec() # start the event loop
```

### Level 2

To add a simple button, here is the code

```Python
from PySide6.QtWidgets import QApplication, QWidget, QMainWindow,QPushButton

import sys

app = QApplication(sys.argv)

window = QMainWindow()
window.setWindowTitle('title1')

button = QPushButton()
button.setText('button1')

window.setCentralWidget(button)
window.show()

app.exec()
```

### Level 3

To organize it better, we group the widget setting into a class

```Python
from PySide6.QtWidgets import QApplication, QWidget, QMainWindow,QPushButton

import sys

class ButtonHolder(QMainWindow): ## class ButtonHolder inherit QMainWindow
    def __init__(self):
        super().__init__()
        self.setWindowTitle('title1')
        button = QPushButton('button1')
        self.setCentralWidget(button)

app = QApplication(sys.argv)
window = ButtonHolder()
window.show()
app.exec()
```

this actually perform the same with above

### Level 4

To make it even more organized, we separate them into files
`button_holder.py`

```Python
from PySide6.QtWidgets import QWidget, QMainWindow,QPushButton

class ButtonHolder(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle('title1')
        button = QPushButton('button1')
        self.setCentralWidget(button)
```

`main.py`

```Python
import sys

from PySide6.QtWidgets import QApplication
from button_holder import ButtonHolder # import the class ButtonHolder from button_holder.py

app = QApplication(sys.argv)
window = ButtonHolder()
window.show()
app.exec()
```

## Step 2 - Signals and Slot

### QPushbutton - Level 1

`clicked` is a signal emitted by QPushButton (Actually it parent QAbstractButton)

```Python
from PySide6.QtWidgets import QApplication, QWidget, QMainWindow,QPushButton

import sys

def button_clicked():
    print('button clicked')

class ButtonHolder(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle('title1')
        button = QPushButton('button1')
        button.clicked.connect(button_clicked) # new statement trigger button_clicked() function to print things
        self.setCentralWidget(button)


app = QApplication(sys.argv)
window = ButtonHolder()
window.show()
app.exec()
```

### QPushbutton - Level 2

Base on the [official doc](https://doc.qt.io/qt-6/qabstractbutton.html), we can know that button can also save it state to the function `button_clicked`

```Python
from PySide6.QtWidgets import QApplication, QWidget, QMainWindow,QPushButton

import sys

def button_clicked(checked): # notice that checked it received as a input which comes from clicked
    print('button clicked' ,checked)

class ButtonHolder(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle('title1')
        button = QPushButton('button1')
        button.setCheckable(True)
        button.clicked.connect(button_clicked)
        self.setCentralWidget(button)


app = QApplication(sys.argv)
window = ButtonHolder()
window.show()
app.exec()
```

### Slider

`Slider` have a `valueChanged` as a signal like button's `clicked`

```Python
from PySide6.QtCore import Qt
from PySide6.QtWidgets import QApplication, QWidget, QMainWindow, QSlider

def slider_change(value):
    print('slider moved' ,value)

app = QApplication()
slider = QSlider(Qt.Horizontal)
slider.setMinimum(1)
slider.setMaximum(100)
slider.setValue(25)
slider.valueChanged.connect(slider_change)
slider.show()
app.exec()
```

## Step 3 - Layout

Put things together.
`widgetholder.py`

```Python
from PySide6.QtCore import Qt
from PySide6.QtWidgets import QWidget, QMainWindow, QSlider, QPushButton, QHBoxLayout, QVBoxLayout

class WidgetHolder(QWidget):
    def __init__(self):
        super().__init__()
        self.setWindowTitle('title1')
        button = QPushButton('button1')
        button.clicked.connect(self.button_clicked) # remember to add self because you are calling function of this class
        slider = QSlider(Qt.Horizontal)
        slider.setMinimum(1)
        slider.setMaximum(100)
        slider.setValue(25)
        slider.valueChanged.connect(self.slider_change)
        layout = QVBoxLayout()
        #layout = QHBoxLayout() # depends on how you want to set the layout
        layout.addWidget(button)
        layout.addWidget(slider)
        self.setLayout(layout)

    def slider_change(self,value): # remember to add self to declare function belong to the class
        print('slider moved' ,value)

    def button_clicked(self):
        print('button clicked')
```

`main.py`

```Python
from PySide6.QtWidgets import QApplication
import sys
from widgetholder import WidgetHolder

app = QApplication(sys.argv)
window = WidgetHolder()
window.show()
app.exec()
```

### GridLayout

```Python
from PySide6.QtWidgets import QWidget, QPushButton, QGridLayout, QSizePolicy

class WidgetHolder(QWidget):
    def __init__(self):
        super().__init__()
        button1 = QPushButton('button1')
        button2 = QPushButton('button2')
        button3 = QPushButton('button3')
        # button3.setSizePolicy(QSizePolicy.Expanding,QSizePolicy.Expanding)
        button4 = QPushButton('button4')
        button5 = QPushButton('button5')
        button6 = QPushButton('button6')
        button7 = QPushButton('button7')

        grid_layout = QGridLayout()
        grid_layout.addWidget(button1,0,0)
        grid_layout.addWidget(button2,0,1,1,2)
        grid_layout.addWidget(button3,1,0,2,1)
        grid_layout.addWidget(button4,1,1)
        grid_layout.addWidget(button5,1,2)
        grid_layout.addWidget(button6,2,1)
        grid_layout.addWidget(button7,2,2)

        self.setLayout(grid_layout)
```

## Step 4 - Menu

Sample code for adding Menu bar in the application

`main.py`

```Python
from PySide6.QtWidgets import QMainWindow, QApplication
import sys
# from widgetholder import WidgetHolder # if you have WidgetHolder from widgetholder.py

class MainWindow(QMainWindow):
    def __init__(self,app):
        super().__init__()
        self.app = app
        self.setWindowTitle('Title1')

        menu_bar = self.menuBar()
        file_menu = menu_bar.addMenu('File')
        quit_action = file_menu.addAction('Quit')
        quit_action.triggered.connect(self.quit_app)

        edit_menu = menu_bar.addMenu('Edit')
        edit_menu.addAction('Copy')
        edit_menu.addAction('Cut')
        edit_menu.addAction('Paste')
        edit_menu.addAction('Undo')
        edit_menu.addAction('Redo')

        # widgetHolder = WidgetHolder() # if you have WidgetHolder from widgetholder.py
        # self.setCentralWidget(widgetHolder)

    def quit_app(self):
        self.app.quit()

app = QApplication(sys.argv)
window = MainWindow(app)
window.show()
app.exec()
```

## MessageBox

https://youtu.be/Z1N9JzNax2k?si=MrBnuwyXc7hCp2Vi&t=6482

## CheckBoxes

`widgetholder.py`

```Python
from PySide6.QtWidgets import QWidget, QGroupBox, QCheckBox,QButtonGroup,QVBoxLayout, QPushButton, QSizePolicy, QGridLayout

class WidgetHolder(QWidget):
    def __init__(self):
        super().__init__()

        os = QGroupBox()
        windows = QCheckBox('Windows')
        linux = QCheckBox('Linux')
        mac = QCheckBox('Mac')

        os_layout = QVBoxLayout()
        os_layout.addWidget(windows)
        os_layout.addWidget(linux)
        os_layout.addWidget(mac)
        os.setLayout(os_layout)

        drinks = QGroupBox('Drinks')
        beer = QCheckBox('Beer')
        juice = QCheckBox('Juice')
        tea = QCheckBox('Tea')
        beer.setChecked(True)

        exclusive_check_group = QButtonGroup(self)
        exclusive_check_group.addButton(beer)
        exclusive_check_group.addButton(juice)
        exclusive_check_group.addButton(tea)
        exclusive_check_group.setExclusive(True)

        drink_layout = QVBoxLayout()
        drink_layout.addWidget(beer)
        drink_layout.addWidget(juice)
        drink_layout.addWidget(tea)
        drinks.setLayout(drink_layout)

        # button1 = QPushButton('button1') # if you want to add the grid buttons
        # button2 = QPushButton('button2')
        # button3 = QPushButton('button3')
        # button3.setSizePolicy(QSizePolicy.Expanding,QSizePolicy.Expanding)
        # button4 = QPushButton('button4')
        # button5 = QPushButton('button5')
        # button6 = QPushButton('button6')
        # button7 = QPushButton('button7')

        # grid_buttons = QGroupBox()
        # grid_layout = QGridLayout()
        # grid_layout.addWidget(button1,0,0)
        # grid_layout.addWidget(button2,0,1,1,2)
        # grid_layout.addWidget(button3,1,0,2,1)
        # grid_layout.addWidget(button4,1,1)
        # grid_layout.addWidget(button5,1,2)
        # grid_layout.addWidget(button6,2,1)
        # grid_layout.addWidget(button7,2,2)
        # grid_buttons.setLayout(grid_layout)

        layout = QVBoxLayout()
        layout.addWidget(os)
        layout.addWidget(drinks)
        # layout.addWidget(grid_buttons)
        self.setLayout(layout)
```

## RadioButtons

`widgetholder.py`

```Python
from PySide6.QtWidgets import QWidget, QGroupBox, QCheckBox,QButtonGroup,QVBoxLayout, QPushButton, QSizePolicy, QGridLayout,QRadioButton

class WidgetHolder(QWidget):
    def __init__(self):
        super().__init__()

        os = QGroupBox()
        windows = QCheckBox('Windows')
        linux = QCheckBox('Linux')
        mac = QCheckBox('Mac')

        os_layout = QVBoxLayout()
        os_layout.addWidget(windows)
        os_layout.addWidget(linux)
        os_layout.addWidget(mac)
        os.setLayout(os_layout)

        drinks = QGroupBox('Drinks')
        beer = QCheckBox('Beer')
        juice = QCheckBox('Juice')
        tea = QCheckBox('Tea')
        beer.setChecked(True)

        exclusive_check_group = QButtonGroup(self)
        exclusive_check_group.addButton(beer)
        exclusive_check_group.addButton(juice)
        exclusive_check_group.addButton(tea)
        exclusive_check_group.setExclusive(True)

        drink_layout = QVBoxLayout()
        drink_layout.addWidget(beer)
        drink_layout.addWidget(juice)
        drink_layout.addWidget(tea)
        drinks.setLayout(drink_layout)

        answers =QGroupBox()
        a = QRadioButton('A')
        b = QRadioButton('B')
        c = QRadioButton('C')
        a.setChecked(True)

        answer_layout = QVBoxLayout()
        answer_layout.addWidget(a)
        answer_layout.addWidget(b)
        answer_layout.addWidget(c)
        answers.setLayout(answer_layout)

        # button1 = QPushButton('button1')
        # button2 = QPushButton('button2')
        # button3 = QPushButton('button3')
        # button3.setSizePolicy(QSizePolicy.Expanding,QSizePolicy.Expanding)
        # button4 = QPushButton('button4')
        # button5 = QPushButton('button5')
        # button6 = QPushButton('button6')
        # button7 = QPushButton('button7')

        # grid_buttons = QGroupBox()
        # grid_layout = QGridLayout()
        # grid_layout.addWidget(button1,0,0)
        # grid_layout.addWidget(button2,0,1,1,2)
        # grid_layout.addWidget(button3,1,0,2,1)
        # grid_layout.addWidget(button4,1,1)
        # grid_layout.addWidget(button5,1,2)
        # grid_layout.addWidget(button6,2,1)
        # grid_layout.addWidget(button7,2,2)
        # grid_buttons.setLayout(grid_layout)

        layout = QVBoxLayout()
        layout.addWidget(os)
        layout.addWidget(drinks)
        layout.addWidget(answers)
        # layout.addWidget(grid_buttons)
        self.setLayout(layout)
```

## Combo Box

`widgetholder.py`

```Python
from PySide6.QtWidgets import QWidget, QComboBox, QPushButton, QVBoxLayout

class WidgetHolder(QWidget):
    def __init__(self):
        super().__init__()

        self.combo_box = QComboBox(self)
        self.combo_box.addItem('A')
        self.combo_box.addItem('B')
        self.combo_box.addItem('C')
        self.combo_box.addItem('D')
        self.combo_box.addItem('E')
        self.combo_box.addItem('F')

        button_current_value = QPushButton('Button')

        layout = QVBoxLayout()
        layout.addWidget(self.combo_box)
        layout.addWidget(button_current_value)
        self.setLayout(layout)
```

## QtDesigner

If you could not find your qt designer, it propably in some path like this `C:\Python311\Lib\site-packages\PySide6\designer.exe`

### QUiLoader

If you use QtDesigner to draft your ui, you need to use QUiLoader to load it

**But user will suffer from loading to ui file everytime they run the application**

```Python
from PySide6 import QtCore
from PySide6.QtUiTools import QUiLoader

loader = QUiLoader()

class UserInterface(QtCore.QObject):
    def __init__(self):
        super().__init__()
        self.ui = loader.load('filename.ui',None)
        self.ui.setWindowTitle('title')
        self.ui.StartButton.clicked.connect(self.startScript)

    def show(self):
        self.ui.show()

    def startScript(self):
        print(self.ui.Target.text(),'running start')
```

### compile ui into py

its recommand to use venv

```PowerShell
python -m venv env
env\Scripts\activate
```

make sure your ui file is here and type

```PowerShell
pyside6-uic target.ui > output.py
```

and make use of the output.py

`main.py`

```Python
import sys
from PySide6 import QtWidgets
from output import MyWidget

class MainUi(QtWidgets.QMainWindow):
    def __init__(self):
        super().__init__()

        self.ui = MyWidget()
        self.ui.setupUi(self)

if __name__ == "__main__":
    app = QtWidgets.QApplication(sys.argv)

    widget = MainUi()
    widget.show()

    sys.exit(app.exec())
```
