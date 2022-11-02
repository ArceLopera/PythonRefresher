In Python, the term packaging refers to putting modules you have written in a standard format, so that other programmers can install and use them with ease.
This involves use of the modules [setuptools](https://pypi.org/project/setuptools/) and [distutils](https://docs.python.org/3/library/distutils.html).
The first step in packaging is to organize existing files correctly. Place all of the files you want to put in a library in the same parent directory. This directory should also contain a file called \__init__.py, which can be blank but must be present in the directory.
This directory goes into another directory containing the readme and license, as well as an important file called setup.py.

- example/
   - LICENSE.txt
   - README.txt
   - setup.py
   - example/
      - \__init__.py
      - example.py
      - example2.py

The next step in packaging is to write the setup.py file.
This contains information necessary to assemble the package so it can be uploaded to PyPI and installed with pip (name, version, etc.).

```py
from distutils.core import setup

setup(
   name='example', 
   version='0.1dev',
   packages=['example',],
   license='MIT', 
   long_description=open('README.txt').read(),
)
```

After creating the setup.py file, upload it to PyPI, or use the command line to create a binary distribution (an executable installer).
To build a source distribution, use the command line to navigate to the directory containing setup.py, and run the command **python setup.py sdist**.
Run **python setup.py bdist** or, for Windows, **python setup.py bdist_wininst** to build a binary distribution.
Use **python setup.py register**, followed by **python setup.py sdist upload** to upload a package.

Finally, install a package with python setup.py install.

## **Packaging for Users**

Most Python users will not want to use this module directly, but instead use the cross-version tools maintained by the Python Packaging Authority. In particular, [setuptools](https://pypi.org/project/setuptools/) is an enhanced alternative to [distutils](https://docs.python.org/3/library/distutils.html).

For Windows, many tools are available for converting scripts to executables. For example, py2exe, can be used to package a Python script, along with the libraries it requires, into a single executable.
PyInstaller and cx_Freeze serve the same purpose.

For Macs, use py2app, PyInstaller or cx_Freeze.
