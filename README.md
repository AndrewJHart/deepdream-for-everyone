
# Deep Dream (for everyone)

Minimal Python/TensorFlow implementation of the DeepDream algorithm originally created by [Alexander Mordvintsev](https://ai.googleblog.com/2015/06/inceptionism-going-deeper-into-neural.html).

<center><a href="https://www.instagram.com/__deep__dreams__/">Daily dose of deep dreams on instagram.</a></center>

## Setup and Installation

First you need to create a virutal environment because by default all versions of python install packages globally & 
this is *very bad*. Consider you use `sudo` and install some python2.7 version of of a package that OSx uses for some
random important task: you just potentially broke it. Ergo, you can create virtualenvs in one of two ways. You can safely 
install the package `virtualenv` globally using `pip install virtualenv` or use built in python 3 flag to create an env.

> Note, this package will not run on python 3.8. Its a tensorflow logging error due
> to the old version of tensorflow I suspect. I did not write this python code
> however, but ported it from a jupiter notebook and while tensorflow versions 
> greater than 1.14 may work, anything as of version 2.0 will not. Too many breaking
> changes. It wouldn't take long to fix the issues as most of the functions have simply
> been moved to new modules or classes. 


Before we start install our python dependencies we will need to install
[caffe](http://caffe.berkeleyvision.org/install_osx.html) and those instructions
are a bit rusty, at least for the OSx link provided. Thus, I will walk
you through the rough bits so you don't have issues with missing homebrew packages
and installation issues. 

> be aware that these are only the steps for OSx

First you need to install [homebrew](http://brew.sh), so paste the
following line into your terminal. 

```bash
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Now brew is installed. You may need to execute the command `$SHELL` before
the brew command is recognized, or you just open a new terminal 
and the `brew` command will be available. Test it by running `brew` and
hitting enter. Onto installing Caffe...

Caffe first says to perform some steps for general dependencies.
However, only the first command works because brew moved the science
keg. So follow these instructions and you should be good to go. 

```
$ brew install -vd snappy leveldb gflags glog szip lmdb

# need the homebrew science source for OpenCV and hdf5
# which no longer exists where Caffe states in homebrew/science
# but now exists in brewsci/science

$ brew tap brewsci/science
$ brew install hdf5 opencv
``` 

The docs mention setting some compiler flags but aren't needed
for the various installations I've attempted on an array of macs
with mojava or catalina at least. Lastly, run this:

```bash
$ brew install protobuf boost 
```

By the way, if you have an NVidia card, see the top of the Caffe
link about installing CUDA. Otherwise, neglect it. This script will run
without it, but will use CPU instead of GPU.


### Configuring python virtual environments.

If you already have virtualenv installed you can still use it,  you specify which version of python you want
to use when you create the virtualenv, by using -p or --python flag, like so:

```bash
$ virtualenv -p python3 venv
```

Next you need to activate your virtual env:

```bash
$ source venv/bin/activate
```

If you **do not have virtualenv installed** python3 gives you a crafty builtin way to do this automatically by passing a flag. 
Make sure you are in the root directory of your project and run these commands to install a python3 virtual env and activate it. 

```bash
$ python3 -m venv venv
$ source venv/bin/activate
```

You will know that your inside your new virtual environment
because the terminal line(s) are prepended with something akin
to this: 

```bash
(venv) $ 
```

When you are done with running your python code later,
you can stop the virtual environment by simply running 

```bash
(venv) $ deactivate

# now your terminal no longer shows (venv)
$ ...
```

## Installing dependencies

In standard python projects all dependencies are installed with pip and saved to a file named `requirements.txt`. This has
been a python standard for as long as I can remember. Therefore, all you need to before being able to run the script is execute this command in your activated python3 virtual environment.

```bash
(venv) $ pip install -r requirements.txt
```

It will take some time, but it will install all of those packages to the `venv/lib/python3.x/site-packages` but you should never modify these.

Now you can run your project 


## Script Usage

To use on the predefined a specific image:

```bash
(venv) $ python deep_dream.py <path_to_the_image>
```


or to use sample data that comes with the project:


```bash
(venv) $ python deep_dream.py
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


#### Original Author who took the google deep dream script (or not) and made readable, maintainable code
 - [Greg (Grzegorz) Surma](https://gsurma.github.io)
 
#### Author of making this project work for everyone
 - [Andrew Hart](https://www.github.com/AndrewJHart)

