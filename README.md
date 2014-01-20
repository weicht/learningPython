learningPython
==============

Not sure of my attempts to upgrade python (using easy_install, pip, home-brew) but this is the setup I have now (17Jan2014)

I think the default Mac version is v2.7.5 and is installed in /usr/bin/python
I think the homebrew version is v2.7.6 and is installed in /usr/local/bin/python

Chriss-MacBook-Pro:~ chrisweicht$ /usr/bin/python --version

Python 2.7.5

Chriss-MacBook-Pro:~ chrisweicht$ /usr/local/bin/python --version

Python 2.7.6

Pip was installed to /usr/local/bin/pip

=> Not sure what utility I used to install pip here but i think it was brew during the 2.7.6 attempt

Make sure the proper pip is being used (/usr/local/bin/pip for me b/c I wanted the v2.7.6)

=> May mean tweaking your PATH variable which I ended up doing within my .bash_profile (later)

<code>
PATH="./:/usr/local/bin:${PATH}"


===
Virtualenv seems to be the de facto standard for python development by creating virtual environments for your project(s).  Virtualenvwrapper is just a wrapper utility that gives a few other convenience utilities:

<code>
sudo pip install virtualenv

<code>
sudo pip install virtualenvwrapper

Set up a folder to hold all your python virtual environments:

<code>
mkdir ~/Envs

=> can be wherever you want them, but this will be where virtualenv operates from

In your .bash_profile, set some env variables and fix the PATH variable (if you want to use a diff python than the default one with OSX):

<code>
PATH="./:/usr/local/bin:${PATH}"

<code>
export PATH

<code>
export WORKON_HOME=~/Envs

<code>
export VIRTUALENVWRAPPER_PYTHON=/usr/local/bin/python

<code>
export VIRTUALENVWRAPPER_VIRTUALENV=/usr/local/bin/virtualenv

<code>
source /usr/local/bin/virtualenvwrapper.sh

###

After making those changes to your .bash_profile, you will need to 'source' it so those vars take effect immediately.

===

Now when you want to create a new python project:

<code>
mkvirtualenv <name of project>

=> This will create the project under your ~/Envs/ folder and "activate" it.  You should/may see your project name prepended to your command line

To work on an existing python project:

<code>
workon <name of project>

=> This is a wrapper for the ‘activate’ process if you were just using virtualenv (ie. source <project>/bin/activate)

While working on a project, all pip install commands will be local to that project:

<code>
pip install flask

=> will only install it to the project structure, not globally

To output a dependencies file (aka “requirements”):

<code>
pip freeze > requirements.txt

=> Note you need to be working on a project when you run this (meaning you used ‘workon’ or the underlying ‘activate’ to make the project active)

To create a new project with a given requirements file:

<code>
pip install -r requirements.txt

=> assuming your reqs file is named “requirements.txt” and is in that dir

To quit working on the project:

<code>
deactivate

To completely remove the project:

<code>
rmvirtualenv <name of project>

List all of the environments.

<code>
lsvirtualenv

Navigate into the directory of the currently activated virtual environment, so you can browse its site-packages, for example.

<code>
cdvirtualenv

Like the above, but directly into site-packages directory.

<code>
cdsitepackages

Shows contents of site-packages directory.

<code>
lssitepackages


