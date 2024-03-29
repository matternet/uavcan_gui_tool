NOTE:  This repo has been decprecated.  UAVCAN GUI Tool has been superceded with [matternet/dronecan_gui_tool]:https://github.com/matternet/dronecan_gui_tool



UAVCAN GUI Tool
===============

[![Travis CI](https://travis-ci.org/UAVCAN/gui_tool.svg?branch=master)](https://travis-ci.org/UAVCAN/gui_tool)
[![Gitter](https://img.shields.io/badge/gitter-join%20chat-green.svg)](https://gitter.im/UAVCAN/general)

UAVCAN GUI Tool is a cross-platform (Windows/Linux/OSX) application for UAVCAN bus management and diagnostics.

[**READ THE DOCUMENTATION HERE**](http://uavcan.org/GUI_Tool).

Read installation instructions:

- [**LINUX**](#installing-on-linux)
- [**WINDOWS**](#installing-on-windows)
- [**OSX**](#installing-on-osx)

![UAVCAN GUI Tool screenshot](screenshot.png "UAVCAN GUI Tool screenshot")

## Installing on Linux

The general approach is simple:

1. Install PyQt5 for Python 3 using your OS' package manager (e.g. APT).
2. Install the application itself from Git via PIP:
`pip3 install git+https://github.com/UAVCAN/gui_tool@master`
(it is not necessary to clone this repository manually).
Alternatively, if you're a developer and you want to install your local copy, use `pip3 install .`.

It also may be necessary to install additional dependencies, depending on your distribution (see details below).

Once the application is installed, you should see new desktop entries available in your desktop menu;
also a new executable `uavcan_gui_tool` will be available in your `PATH`.
If your desktop environment doesn't update the menu automatically, you may want to do it manually, e.g.
by invoking `sudo update-desktop-database` (command depends on the distribution).

It is also recommended to install Matplotlib - it is not used by the application itself,
but it may come in handy when using the embedded IPython console.

### Debian-based distributions

```bash
sudo apt-get install -y python3-pip python3-setuptools python3-wheel
sudo apt-get install -y python3-numpy python3-pyqt5 python3-pyqt5.qtsvg git-core
sudo pip3 install git+https://github.com/UAVCAN/gui_tool@master
```

#### Troubleshooting

If installation fails with an error like below, try to install IPython directly with `sudo pip3 install ipython`:

> error: Setup script exited with error in ipython setup command:
> Invalid environment marker: sys_platform == "darwin" and platform_python_implementation == "CPython"

If you're still unable to install the package, please open a ticket.

### RPM-based distributions

*Maintainers wanted*

## Installing on Windows

In order to install this application,
**download and install the latest `.msi` package from here: <https://files.zubax.com/products/org.uavcan.gui_tool/>**.

### Building the MSI package

These instructions are for developers only. End users should use pre-built MSI packages (see the link above).

First, install dependencies:

* [WinPython 3.4 or newer, pre-packaged with PyQt5](http://winpython.github.io/).
Make sure that `python` can be invoked from the terminal; if it can't, check your `PATH`.
* Windows 10 SDK.
[Free edition of Visual Studio is packaged with Windows SDK](https://www.visualstudio.com/).

Then, place the `*.pfx` file containing the code signing certificate in the outer directory
(the build script will search for `../*.pfx`).
Having done that, execute the following (the script will prompt you for password to read the certificate file):

```dos
python -m pip uninstall -y uavcan
python -m pip uninstall -y uavcan_gui_tool
python setup.py install
python setup.py bdist_msi
```

Collect the resulting signed MSI from `dist/`.

## Installing on OSX

OSX support is a bit lacking in the way that installation doesn't create an entry in the applications menu,
but this issue should be fixed someday in the future.
Other than that, everything appears to function more or less correctly.
If you have a choice, it is recommended to use Linux or Windows instead,
as these ports are supported much better at the moment.

### Homebrew option

* Install the Homebrew package manager for OSX.
* make sure to install python 3.6.5; 3.7 DOES NOT WORK!
    * If python 3 version is currently 3.7 use 'brew uninstall python' to remove it
* Run the following commands:

```bash
brew install https://raw.githubusercontent.com/Homebrew/homebrew-core/f2a764ef944b1080be64bd88dca9a1d80130c558/Formula/python.rb
pip3 install PyQt5
pip3 install git+https://github.com/matternet/uavcan_gui_tool
uavcan_gui_tool
```

### MacPorts option

Install XCode from App Store, install MacPorts from <https://www.macports.org/install.php>,
then run the commands below.
If you're prompted to install Command Line Developer Tools, agree.

```bash
sudo port selfupdate
sudo port install curl-ca-bundle py35-pip py35-pyqt5 py35-numpy
sudo python3.5 -m pip install git+https://github.com/UAVCAN/gui_tool@master
```

We would like to provide prebuilt application packages instead of the mess above.
Contributions adding this capability would be welcome.

## Development

### Releasing new version

First, deploy the new version to PyPI. In order to do that, perform the following steps:

1. Update the version tuple in `version.py`, e.g. `1, 0`, and commit this change.
2. Create a new tag with the same version number as in the version file, e.g. `git tag -a 1.0 -m v1.0`.
3. Push to master: `git push && git push --tags`

Then, build a Windows MSI package using the instructions above, and upload the resulting MSI to
the distribution server.

### Code style

Please follow the [Zubax Python Coding Conventions](https://kb.zubax.com/x/_oAh).
