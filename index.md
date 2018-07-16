---
title: "Getting started with the Arable API"
keywords: sample homepage
tags: [getting_started, python]
sidebar: home_sidebar
permalink: index.html
summary: These brief instructions will help you get started quickly with using the Arable API. We also provide some more detailed applications and workflows that use Arable device data.
---

{% include note.html content="These instructions assume basic familiarity with shell environments, but that you haven't used python before on your device." %}


## Setting up your environment
 
 {% include note.html content="Arable uses Python version 2.7" %}

### 1. Install python and jupyter

* Install [Homebrew](https://brew.sh/), a package installer for OS X.

* Install Python version 2.7:

```
> brew install python@2
```

* Install Jupyter:

```
> brew install jupyter
```

* Pip install numpy, pandas, and matplotlib:

```
> pip install numpy pandas matplotlib
```

{% include note.html content="Pip may ask you to upgrade to pip 10. As of this writing, we have found pip 10 problematic." %}

* Install [Sublime Text](http://www.sublimetext.com/), a text editor.

###  2. Set up your shell environment.

{% include note.html content="If you are already used to editing files and using a unix shell, then you can skip these simple instructions and jump to the next section." %}

* Make some changes to your environment. 

```
echo 'alias ipy="jupyter notebook"' >> ~/.bashrc
```
```
echo 'export EDITOR="subl -w"' >> ~/.bashrc
```

* Add your Arable credentials to your environment.

```
echo 'export ARABLE_EMAIL="friendof@arable.com"' >> ~/.bashrc
```
```
echo 'export ARABLE_PASSWD="agrofuturism"' >> ~/.bashrc
```
```
echo 'export ARABLE_TENANT="franz_hydro"' >> ~/.bashrc
```

In the terminal type `. .bashrc` to activate these parameters in the current shell.

In the terminal type `subl .bash_profile` and add the following text, then save and close.

```
#source .bashrc
if [ -f ~/.bashrc ]; then
  . ~/.bashrc
fi

export PATH=/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
```

In the terminal type `. .bash_profile`


### 3. Install the Arable python client 

While not strictly necessary, you may find the Arable python client useful to help get you going:

```
pip install arable
``` 

Navigate to a project folder where you can start developing.

```
mkdir ~/Arable; cd ~/Arable
```

Download [arable_physics.py](/_jupyter/arable_physics.py) and move it into your project folder to access these helpful functions.

When you are ready to start the examples type `ipy` in your terminal and try some of the [examples](/examples_landing_page.html)!

### NB: physics.py is in the _jupyter folder
