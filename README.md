<h3 align="center">
  <img src="assets/deep_dream_icon_web.png" width="300">
</h3>

# Deep Dream

Minimal Python/TensorFlow implementation of the DeepDream algorithm originally created by [Alexander Mordvintsev](https://ai.googleblog.com/2015/06/inceptionism-going-deeper-into-neural.html).

<center><a href="https://www.instagram.com/__deep__dreams__/">Daily dose of deep dreams on instagram.</a></center>

## Setup and Installation

First you need to create a virutal environment because by default all versions of python install packages globally & 
this is *very bad*. Consider you use `sudo` and install some python2.7 version of of a package that OSx uses for some
random important task: you just potentially broke it. Ergo, you can create virtualenvs in one of two ways. You can safely install the package `virtualenv` globally, and to create a python2.7 environment run this. 

> Note this is a python 3 script, so this is for example in case you need it later. 

### python 2.7 virtualenv installation 

```bash
$ pip install virtualenv 

$ virutalenv venv
```

This will create a virtual env in a folder name `venv` in your project and this is essentially reinstalling python in a non-global scope. If you open venv you will see what a python installation looks like. 

Next you need to activate your virtual env (ensuring you're still in same root directory of your project)

```bash
$ source venv/bin/activate
```

and your terminal will change to this to make you aware you are in a virtualenv, prefixing your commands with the name of your env in parenthesis like so

```bash
(venv) $ 
```

### python3 and above virtual environments.

If you already have virtualenv installed you can still use it like above except you specify which version of python you want
to use when you create the virtualenv like so

```bash
$ virtualenv -p python3 venv
```
And activate is the same way as before `source venv/bin/activate` then run your pip commands.

If you **do not have virtualenv installed** python3 gives you a crafty builtin way to do this automatically by passing a flag. 
Make sure you are in the root directory of your project and run these commands to install a python3 virtual env and activate it. 

```bash
$ python3 -m venv venv
$ source venv/bin/activate
```
 
When you are done with running your python code you can kill the virutal environment by simply running 

```bash
$ deactivate
```

## Installing dependencies

In standard python projects all dependencies are installed with pip and saved to a file named `requirements.txt`. This has
been a python standard for as long as I can remember. Therefore, all you need to before being able to run the script is execute this command in your activated python3 virtual environment.

```bash
(venv) $ pip install -r requirements.txt
```

It will take some time, but it will install all of those packages to the `venv/lib/python3.x/site-packages` but you should never modify these.

Now you can run your project 


## Usage

To use on the predefined .jpg image:

```bash
(venv) $ python3 deep_dream.py <path_to_the_image>
```

or

```bash
(venv) $ python3 deep_dream.py
```

to perform on the random image.

## How does it work?

We are using **Inception5h** model which was designed to classify images. 

During the classification process we are providing input images and using gradient descent to adapt weights to the images through filters. 

**DeepDream** algorithm does the opposite. It adapts the input images to match the network weights with **gradient ascent** which results in visualizing network filters on the input images giving them psychodelic look.



## Results

![src deep_dream_0](/examples/deep_dream_0.jpeg)

<img src="examples/deep_dream_0.jpeg">
<img src="examples/deep_dream_1.jpeg">
<img src="examples/deep_dream_2.jpeg">
<img src="examples/deep_dream_3.jpeg">
<img src="examples/deep_dream_4.jpeg">
<img src="examples/deep_dream_5.jpeg">


## Author

**Greg (Grzegorz) Surma**

[**PORTFOLIO**](https://gsurma.github.io)

[**GITHUB**](https://github.com/gsurma)

[**BLOG**](https://medium.com/@gsurma)

<a href="https://www.paypal.com/paypalme2/grzegorzsurma115">
  <img alt="Support via PayPal" src="https://cdn.rawgit.com/twolfson/paypal-github-button/1.0.0/dist/button.svg"/>
</a>

