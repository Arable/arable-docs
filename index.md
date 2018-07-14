---
title: "Getting started with the Arable API"
keywords: sample homepage
tags: [getting_started, python]
sidebar: home_sidebar
permalink: index.html
summary: These brief instructions will help you get started quickly with using the Arable API. We also provide some more detailed applications and workflows that use Arable device data.
---

{% include note.html content="These instructions assume basic familiarity with shell environments, but that you haven't used python before on your device." %}


## Setting up your environment.
 
 {% include note.html content="Arable uses Python version 2.7" %}

### 1. Install the Arable python client 

```
pip install arable
``` 

Place "physics.py" in a suitable place in your path to access these helpful functions 

(Note? why isn't this part of the arable client??)

The notebook .ipynb can be opened in the Jupyter environment.  

###  2. Set up your shell environment.

{% include note.html content="If you are already used to editing files and using a unix shell, then you can skip these simple instructions and jump to the next section." %}

* Make some changes to your environment. 

```
echo 'alias ipynb="jupyter notebook"' >> ~/.bashrc
```
```
echo 'export EDITOR="subl -w" >> ~/.bashrc
```

In the terminal type `. .bashrc`

In the terminal type `subl .bash_profile` and add the following text, then save and close.

```
#source .bashrc
if [ -f ~/.bashrc ]; then
  . ~/.bashrc
fi

export PATH=/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
```

In the terminal type `. .bash_profile`

### 3. Install python and jupyter

* Install [Homebrew](https://brew.sh/)

* Install Python version 2.7:

```
> brew install python@2
```

* Install Jupyter:

```
> brew install jupyter
```

* Find a suitable folder and copy the `ipynb` file over to it.

```
> mkdir lib
```
 Add `physics.py` to `/lib`

```
> ipynb
```

A new window should open in your browser!  Update your username, password, and tenant and start playing with data!

[FIN]


