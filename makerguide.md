#Creating a PIP package guide 

This guide a concise how to for setting up the  **pibot** python modules for distributed through **PyPi** (*Python Package Index) so that it can be installed using **PIP** )recursive acronym - Pip Installs Packages).

###USeful Links
- **For using PIP** [Official PIP install guide](https://pip.pypa.io/en/latest/reference/pip_install/)
- **For creating packages and distributing through PyPi:** [Packagingand Distributing Projects] (https://packaging.python.org/distributing/)
- Guide to Python Packages: [Packages] (http://www.network-theory.co.uk/docs/pytut/Packages.html)
- A devs experience in making packages and [Uploading To PyPi](https://tom-christie.github.io/articles/pypi/)

###Getting Started.
The user guide has got me as far as preparing the package that I have now hosted on github:[https://github.com/pi-bot/pibot-pkg](https://github.com/pi-bot/pibot-pkg)
See the repo for setup files etc. Will now go through steps for cloning this and uploading to PiPy. 

```
git clone https://github.com/pi-bot/pibot-pkg.git
```

Then we go into the root directory and build the package .zip file for uploading to PyPi.

Once Installed the package exists on the Raspian system here:

```
/usr/lib/python2.7/dist-packages/
```

This is in all users global **$PYTHONPATH** so that modules can then be imported. Issue I was having was getting **IDLE** to access the modules.  We can check the $PYTHONPATH of the application by opening IDLE and then:
```
>>> import sys
>>> print sys.path
```
Output is 
```
Put output here
```

OK so now lets import the module.
###Using Test PyPi Server
This [guide](https://wiki.python.org/moin/TestPyPI) explains how to set up a test server to practice uploading/distributing packages through PyPi.  My Project is in Beta so its appropriate to use this.

My **~/.pypirc** file is made by 

```
vim ~/.pypirc
```


```
[distutils]
index-servers=
    pypi
    pypitest

[pypitest]
repository = https://testpypi.python.org/pypi
username = HarryGeeTest
password = harryTestxxx

[pypi]
repository = https://pypi.python.org/pypi
username = <your user name goes here>
password = <your password goes here>
```

Then use the rest of the guide to upload your package. 

###Register Package
```
python setup.py register -r https://testpypi.python.org/pypi
```
Next thing is to create the distribution file to upload.

```
python setup.py sdist
```
Then upload it ...
```
python setup.py sdist upload -r https://testpypi.python.org/pypi
```
**N.B.** The guide misses out the **sdist** from the last command that threw an error the first time I tried.

```
Server response (200):OK
```
Great ! We're in business:)

### Downloading and testing 
So That covers the installation now lets download and test. 
```
pip install -i https://testpypi.python.org/pypi pibot
```


**NB** Update the version number everytime you make changes to the package. 
