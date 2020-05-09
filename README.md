<img width="30" alt="Label-Images-Tool Logo" src="/resources/icons/app.png"> Label-Images-Tool
========

[![PyPi Label](https://img.shields.io/pypi/v/labelimg.svg "PyPi Label")](https://pypi.python.org/pypi/labelimg) [![Build dLabel](https://img.shields.io/travis/tzutalin/labelImg.svg "Build Label")](https://travis-ci.org/tzutalin/labelImg)

Label-Images-Tool is a graphical image annotation tool and label object bounding boxes in images.
It is written in Python and uses Qt for its graphical interface.

Annotations are saved as TXT files in [YOLO](https://pjreddie.com/darknet/yolo/ "YOLO: Real-Time Object Detection") format or as XML files in [PASCAL VOC](http://host.robots.ox.ac.uk/pascal/VOC/ "The PASCAL Visual Object Classes Homepage") format (used by [ImageNet](http://www.image-net.org/ "ImageNet homepage")).

<img width="400" alt="Demo printscreen" src="https://raw.githubusercontent.com/tzutalin/labelImg/master/demo/demo3.jpg">
<img width="400" alt="Demo printscreen" src="https://raw.githubusercontent.com/tzutalin/labelImg/master/demo/demo.jpg">

[Watch a demo video](https://youtu.be/p0nR2YsCY_U "Watch a demo video")









## Installation


### Build from source


Linux/Ubuntu/Mac requires at least [Python 2.6](https://www.python.org/getit/) and has been tested with [PyQt 4.8](https://www.riverbankcomputing.com/software/pyqt/intro). However, [Python 3 or above](https://www.python.org/getit/) and [PyQt5](https://pypi.org/project/PyQt5/) are strongly recommended.


#### Ubuntu Linux

Python 2 + Qt4
```
sudo apt-get install pyqt4-dev-tools
sudo pip install lxml
make qt4py2
python labelImg.py
python labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

Python 3 + Qt5 (Recommended)
```
sudo apt-get install pyqt5-dev-tools
sudo pip3 install -r requirements/requirements-linux-python3.txt
make qt5py3
python3 labelImg.py
python3 labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

#### macOS

Python 2 + Qt4
```
brew install qt qt4
brew install libxml2
make qt4py2
python labelImg.py
python labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

Python 3 + Qt5 (Recommended)
```
brew install qt  # Install qt-5.x.x by Homebrew
brew install libxml2

or using pip

pip3 install pyqt5 lxml # Install qt and lxml by pip

make qt5py3
python3 labelImg.py
python3 labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

Python 3 Virtualenv (Recommended)

Virtualenv can avoid a lot of the QT / Python version issues
```
brew install python3
pip3 install pipenv
pipenv run pip install pyqt5==5.13.2 lxml
pipenv run make qt5py3
python3 labelImg.py
[Optional] rm -rf build dist; python setup.py py2app -A;mv "dist/labelImg.app" /Applications
```

Note: The Last command gives you a nice .app file with a new SVG Icon in your /Applications folder. You can consider using the script: build-tools/build-for-macos.sh

#### Windows

Install [Python](https://www.python.org/downloads/windows/), [PyQt5](https://www.riverbankcomputing.com/software/pyqt/download5) and [install lxml](http://lxml.de/installation.html).

Open cmd and go to the [labelImg](#labelimg) directory
```
pyrcc4 -o lib/resources.py resources.qrc
For pyqt5, pyrcc5 -o libs/resources.py resources.qrc

python labelImg.py
python labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

#### Windows + Anaconda

Download and install [Anaconda](https://www.anaconda.com/download/#download) (Python 3+)

Open the Anaconda Prompt and go to the [labelImg](#labelimg) directory

```
conda install pyqt=5
pyrcc5 -o libs/resources.py resources.qrc
python labelImg.py
python labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

### Get from PyPI but only python3.0 or above

```
pip3 install labelImg
labelImg
labelImg [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

### Use Docker

```
docker run -it \
--user $(id -u) \
-e DISPLAY=unix$DISPLAY \
--workdir=$(pwd) \
--volume="/home/$USER:/home/$USER" \
--volume="/etc/group:/etc/group:ro" \
--volume="/etc/passwd:/etc/passwd:ro" \
--volume="/etc/shadow:/etc/shadow:ro" \
--volume="/etc/sudoers.d:/etc/sudoers.d:ro" \
-v /tmp/.X11-unix:/tmp/.X11-unix \
tzutalin/py2qt4

make qt4py2;./labelImg.py
```

You can pull the image which has all of the installed and required dependencies. [Watch a demo video](https://youtu.be/nw1GexJzbCI)


## Usage

### Steps (PascalVOC)

1. Build and launch using the instructions above.
2. Click 'Change default saved annotation folder' in Menu/File
3. Click 'Open Dir'
4. Click 'Create RectBox'
5. Click and release left mouse to select a region to annotate the rect
   box
6. You can use right mouse to drag the rect box to copy or move it

The annotation will be saved to the folder you specify.
You can refer to the below hotkeys to speed up your workflow.

### Steps (YOLO)

1. In `data/predefined_classes.txt` define the list of classes that will be used for your training.
2. Build and launch using the instructions above.
3. Right below "Save" button in the toolbar, click "PascalVOC" button to switch to YOLO format.
4. You may use Open/OpenDIR to process single or multiple images. When finished with a single image, click save.

A txt file of YOLO format will be saved in the same folder as your image with same name. A file named "classes.txt" is saved to that folder too. "classes.txt" defines the list of class names that your YOLO label refers to.

Note:

- Your label list shall not change in the middle of processing a list of images. When you save an image, classes.txt will also get updated, while previous annotations will not be updated.

- You shouldn't use "default class" function when saving to YOLO format, it will not be referred.

- When saving as YOLO format, "difficult" flag is discarded.

Create pre-defined classes
~~~~~~~~~~~~~~~~~~~~~~~~~~

You can edit the [data/predefined\_classes.txt](https://github.com/tzutalin/labelImg/blob/master/data/predefined_classes.txt) to load pre-defined classes

## Hotkeys

+------------+--------------------------------------------+
| Ctrl + u   | Load all of the images from a directory    |
+------------+--------------------------------------------+
| Ctrl + r   | Change the default annotation target dir   |
+------------+--------------------------------------------+
| Ctrl + s   | Save                                       |
+------------+--------------------------------------------+
| Ctrl + d   | Copy the current label and rect box        |
+------------+--------------------------------------------+
| Space      | Flag the current image as verified         |
+------------+--------------------------------------------+
| w          | Create a rect box                          |
+------------+--------------------------------------------+
| d          | Next image                                 |
+------------+--------------------------------------------+
| a          | Previous image                             |
+------------+--------------------------------------------+
| del        | Delete the selected rect box               |
+------------+--------------------------------------------+
| Ctrl++     | Zoom in                                    |
+------------+--------------------------------------------+
| Ctrl--     | Zoom out                                   |
+------------+--------------------------------------------+
| ↑→↓←       | Keyboard arrows to move selected rect box  |
+------------+--------------------------------------------+

#### Verify Image

When pressing space, the user can flag the image as verified, a green background will appear.
This is used when creating a dataset automatically, the user can then through all the pictures and flag them instead of annotate them.

#### Difficult

The difficult field is set to 1 indicates that the object has been annotated as "difficult", for example, an object which is clearly visible but difficult to recognize without substantial use of context.
According to your deep neural network implementation, you can include or exclude difficult objects during training.

### How to reset the settings

In case there are issues with loading the classes, you can either:

1. From the top menu of the labelimg click on Menu/File/Reset All
2. Remove the `.labelImgSettings.pkl` from your home directory. In Linux and Mac you can do: 
`rm ~/.labelImgSettings.pkl`


### How to contribute

Send a pull request

### License

`Free software: MIT license <https://github.com/tzutalin/labelImg/blob/master/LICENSE>`_

### Original GitHub project:
[tzutalin/labelImg](https://github.com/tzutalin/labelImg "tzutalin/labelImg repository")
