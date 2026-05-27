**Useful Python libraries**

**Working with files**

Library OS :  $ import os

` `we import this library to be able to work with folders and files on the system, path actually belongs to this library

- set the path

`         `$ path = “ dataset folder ”   -à the folder is in the same root folder as python code

`         `$ path = r” E:\Workspace\DSS\src\dataset folder”   -à the folder is not in the same root folder as python code   (r prefix here indicates that special characters in this string should not be evaluated)

- Get all filenames in your path

  $ files = os.listdir(path)  -à this will return us a list of filenames

- Iterate over files

  For file in files 

  `  `Print(file)

- get all files with specific file extensions

`             `filename = [f for f in files if ".meta" in f]

- get the name of a file (without extension)

  basename = os.path.basename(file)

- make a new path to a file name we have

`             `img\_path = os.path.join(path , name + ".png")     / path is the path we had 

`	`/ name is a new file name

- separate the filename from extension

  filename[4].split(“.”)[0]

- iterate over the filenames with index          

  for index , f  in enumerate(filename[22:]):                  

  `  `if index == 5	

  `    `break	 

  `  `print(index)

  `  `print(f)

`            `for  index,f   in filename [ : 5]:   --à index starts from 0

`            `print(file)

- work with content of a file  (Dictionaries)

  title = [v for k,v in meta.items() if k =="Subject disorder status" ]

- file.**append** (new file)

**Pathlib**

Pathlib library -à this library can also be used for working with files 

- $ from pathlib import path
- My\_path = Path(path of our dataset folder)  à we create a path object called My\_path
- Get all filenames with specific extension

  $import glob

  filenames = glob.glob(path + “/.\*meta”)   **or**   filename = print(str(My\_path / “\*.meta”)) 

- Separate filename from its extension

  File = My\_path / “100.meta”

  File.stem()  -à returns the file extension-à .meta


**Loading images**

Imageio library à $ pip install imageio

`                               `-à$ import imageio.v3 as io

- img = io.imread(imp\_path)
- saving the image 

  io.imwrite(‘img.png’ , img)


Opencv library à $ pip install opencv-python

- $ import cv2
- Imag = cv2.imread(img\_path)      
- Img = cv2.cvtColor(imag , cv2.COLOR\_BGR2RGB)    à opencv shows images in BGR color So here we concert it to RGB

Scikit-image library  à $ pip install scikit-image

`                                       `à$ import skimage

- Img = skimage.io.imread(imag\_path)
- img = skimage.io.imread(img\_path, as\_gray=True) -à load image as grayscale


Pillow library à $ pip install pillow

`                           `à $ from PIL import Image

- img = Image.open(imag\_path)

Matplotlib libraryà $ pip install matplotplib

`                                `à $ import matplotlib.pyplot as plt 

- **subplots** : With the subplot() function you can draw multiple plots in one figure


**Json library** is a built in library in python  -à import json

- with open (path to the json file or a metadata file) as f:

  `    `file = josn.load(f)

- **img [ : , : , 0 ]**    --à this gives us the first color channel (Red) of all pixels, actually  

  `                                 `shows the image in red color

  ![](Aspose.Words.d7eb5b1d-e047-437b-888e-b504b38396f1.001.png)	

  `                 `dimensions of the image (width, height , depth(color))	

- **np.mean( img , axis = -1 )**   --à get the avg of all values in the last dimention (color 
  **
  `                                                         `dimention)

- **np.max** ( **img , axis  = -1**)

- axis = 1 à width , axis = 2 -à height , axis = 3 à color channel



- **Flammkucken** is a library that you can use to store hdf5 files (that u can use as a container to store different file types**)**

  **Import flammkuchen as f1**

  **d = {**

  ‘tabular’ : pd.dataframe(np.random.random(20,40)) **,**   à random tabular data

  ‘json’ : dict(name = ‘sahel’ , age = ‘12’)

  **}**

  **f1.save**(“my\_hdf5\_file.h5” , d)  -à we can use arbitrary file extension

  **f1.meta**(“my\_hdf5\_file.h5”)

  **f1.load**(“my\_hdf5\_file.h5” , “/tabular”)  -àyou can load one of the files in your container




**Plotting**

- **plt.imshow**(img , cmap = ‘grey’ , alpha =)    -à show the image in grey scale

- **plt.title**(title[0] , fontdict={'fontsize' : 9} , pad=5)

- remove the axis labels of the plot

  **plt.axis**('off')

- **plt.rcParams**["figure.figsize"] = (5,5)
- show the final plot

  **plt.show**()

- **Bar plot**

  plt.bar([0, 1, 2, 3], [img\_tif\_size, img\_png\_size, img\_jpg90\_size, img\_jpg10\_size])

  ![](Aspose.Words.d7eb5b1d-e047-437b-888e-b504b38396f1.002.png)

  `	`reference to bars and what to show for each bar

- Lables on the axis

  **plt.xticks**([0, 1, 2, 3], [".tif", ".png", ".jpg (90)", ".jpg (10)"])

  **plt.ylabel**("File size [bytes]")

**Subplot**

- make 4 subplots in one figure

  **plt.subplot**(**2,2)**  --à the plot with 4 subplots --à 2 subplot in rows and 2 in columns 

- we can go over subplots of a plot one by one in a for loop by

  **plt.subplot(2,2,1)**   -à here we are just telling to draw the first subplot of our plot and all following commands will be applied for this subplot


- **How to overlay segmentation masks on an image ?**

`             `Just plot them one after another

`             `plt.imshow(img)

`             `plt.imshow(segment)

- How to convert an image from RGB to grey scale?
1. Average method

   For each pixel we average the R,G and B values

1. Luminosity method

   For each pixel we average the R,G and B values **BUT** with given weights

   And give a higher weight to the green value (G)

1. Lightness method

   For each pixel get addition of Max and Min of R, G and B values devided by 2













**DSS**

**Python Packaging**

The **directory structure for your python project** on GitHub is very important :

![](Aspose.Words.d7eb5b1d-e047-437b-888e-b504b38396f1.003.png)![](Aspose.Words.d7eb5b1d-e047-437b-888e-b504b38396f1.004.png)![](Aspose.Words.d7eb5b1d-e047-437b-888e-b504b38396f1.005.png)![](Aspose.Words.d7eb5b1d-e047-437b-888e-b504b38396f1.006.png)![Text

Description automatically generated with medium confidence](Aspose.Words.d7eb5b1d-e047-437b-888e-b504b38396f1.007.png)

**Setup.py** -à essential for python packaging , if you want to make your python script installable by others you should have a setup.py that you define metadata about your python package (name =” “ , version = “ “ , …..)

![](Aspose.Words.d7eb5b1d-e047-437b-888e-b504b38396f1.008.png)

**Package name** à is your python package (python function)

**\_init.py\_** à make your python package installable and importable by others

**\_main.py\_**   à execute your package as a module

**function.py**  à is your python script (function)

![](Aspose.Words.d7eb5b1d-e047-437b-888e-b504b38396f1.009.png)if you want **to install your GitHub repository as a python package** , you have to run one of  these commands in the working directory of your repo :

1. **python -m pip install .       à** this will look inside the current directory to find the setup.py file
1. **python -m pip install git + Repo URL .git  à** this will look into remote GitHub repo URL to find the setup.py file

both of these approaches will look for setup.py  for packaging

If you want to import your package 

**Python -c  “import snowflake”**

If you want to run the package 

**Python -m  “snowflake**

\*\*\*\* metadata files (.meta) are actually json files 


**PYQT**

**What is QT ?**

**Qt framework** is a popular solution for GUI development. Qt is **a C++framework** for developing graphical user interfaces and **cross-platform applications**, both desktop and [embedded](https://www.sam-solutions.com/services/embedded/embedded-software-development/). The framework can function on different types of software and hardware.

It offers a special software development language: Qt Modeling Language*(**QML**)*

In addition, it can be bound with other languages such as:

- [Java](https://www.sam-solutions.com/services/technologies/java/)
- **Python**
- [PHP](https://www.sam-solutions.com/services/technologies/php/)

The Qt Integrated Development Environment (**IDE**) is known as **Qt Creator**.

Thanks to the widget toolkit, programmers can code straightaway in C++



**What is PYQT ?**

**PyQt** is a set of Python binding for the open-source Qt Framework from C++ that can be used to create Desktop Graphical User Interfaces.

PyQt5 provides a binding for only the 5.x versions. As a result, PyQt5 is not backward compatible with the deprecated modules of the older version

PyQt is a module to make desktop software with Python. This works on all desktop systems including Mac OS X, Windows and Linux. These module includes:
*QtCore, QtGui, QtWidgets, QtMultimedia, QtBluetooth, QtNetwork, QtPositioning, Enginio, QtWebSockets, QtWebKit, QtWebKitWidgets, QtXml, QtSvg, QtSql and QtTest*.

- **QtWidgets** has **a many UI widgets** like buttons, labels, textinput and other things you’d see in a desktop window.

PyQt gives you all the complex functionalities of C++ Qt while allowing swift development in Python.

PyQt is widely used for creating large-scale GUI-based programs.

PyQT gives you widgets to create complex GUIs. In fact, **everything in PyQT** (buttons, input fields, checkboxes, and Radio boxes) **is a widget.**

PyQt can be installed using the command : >>> **pip install PyQt5**

This is a simple PyQt program:

import sys

from PyQt5.QtWidgets import **QApplication, QWidget**

if \_\_name\_\_ == "\_\_main\_\_":

`    `**app = QApplication(sys.argv)**

`    `w = QWidget()

`    `**w.resize**(300,300)

`    `**w.setWindowTitle**("Guru99")

`    `w.show()

`    `sys.exit(app.exec\_())

**app = QApplication(sys.argv)**   ---à  Here, you are creating an object of the QApplication class. This step is a necessity for PyQt5; every UI app must create an instance of QApplication.

sys.argv is the list of command-line parameters that you can pass to the application when launching it through the shell or while automating the interface or if you do not pass any arguments you can replace with **app = QApplication([])**

**w = QWidget()**   -à  Next, we make an object of the QWidget class. QWidget is the base class of all UI objects in Qt, and virtually everything you see in an app is a widget. That includes dialogs, texts, buttons, bars, and so on. The feature that allows you to design complex user interfaces is that the widgets can be nested, i.e., you can have a widget inside a widget. Here, you should remember that widgets could be nested together, **the outermost widget** (i.e., the widget with no parent) **is called a Window.**

**sys.exit(app.exec\_())** ----à The app.exec\_() method starts the Qt/C++ event loop. As you know, PyQt is largely written in C++ and uses the event loop mechanism to implement parallel execution. app.exec\_() passes the control over to Qt which will exit the application only when the user closes it from the GUI. That is why ctrl+c will not exit the application as in other python programs. 

**Events :**

In GUI based applications, functions are executed based on the actions performed by the user, like hovering over an element or clicking a button. These actions are called **events**. Recall that the app.exec\_() method transfers control to the Qt **event-**loop. This is what the event loop is there for: to listen for events and perform actions in response.

Whenever an event occurs, like a user clicking a button, the corresponding Qt widget raises a **signal**. These signals can be connected to python functions (like the dialog function in this example) so that the function is executed when a signal is triggered. These functions are called **slots** in Qt lingo.

` `the basic syntax to trigger a slot function in response to the signal from an event is as follows  :    >>>> **widget.signal.connect(slot)**

Which means that whenever a **signal** is triggered by a **widget**, the connected **slot** function will be executed

**PyQtgraph:**

PyQtGraph is a graphics and user interface library for Python that provides functionality commonly required in designing and science applications. **Its primary goals are to provide fast, interactive graphics for displaying data (plots, video, etc.)** and **second is to provide tools to aid in rapid application developmen**t (for example, property trees such as used in Qt Designer).

**One of the major strengths of Python is in exploratory data science and visualization, using tools such as Pandas, numpy, sklearn for data analysis and matplotlib plotting.** Buiding GUI applications with PyQt gives you access to all these Python tools directly from within your app, allowing you to build complex data-driven apps and interactive dashboards.

While it is possible to embed matplotlib plots in PyQt the experience does not feel entirely *native*. For simple and highly interactive plots you may want to consider using PyQtGraph instead. **PyQtGraph is built on top of Qt's native QGraphicsScene giving better drawing performance, particularly for live data, as well as providing interactivity and the ability to easily customize plots with Qt graphics widgets.**

To be able to use PyQtGraph with PyQt you first need to install the package 

$ pip install pyqtgraph















