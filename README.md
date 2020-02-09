
# Deep Dream for everyone

Minimal Python/TensorFlow implementation of the DeepDream algorithm originally created by [Alexander Mordvintsev](https://ai.googleblog.com/2015/06/inceptionism-going-deeper-into-neural.html).

## Setup and Installation

This will work on OSx and linux if you use homebrew for linux. Otherwise you can install 
the brew packages via apt-get. Caffe does provide installation instructions
for linux but i have not tested them. 

> note that I was able to get this running on an nVidia Jetson nano
> running ubuntu. By using `apt-get` and a specific version of Tensorflow
> built for linux + GPU. All necessary python dependencies are in `requirements.txt`,
> however you will want to remove all 3 tensorflow packages from `requirements.txt`
> and point your jetson to this url for tensorflow v1.15 
> `pip3 install --pre  https://developer.download.nvidia.com/compute/redist/jp/v43/https://developer.download.nvidia.com/compute/redist/jp/v43/tensorflow-gpu/tensorflow_gpu-1.15.0+nv19.12-cp36-cp36m-linux_aarch64.whl`
> This will install tensorflow 1.15.0, then you can install the remaining
> python dependencies.
>
> If you need help, please reach out :) 

First you need to create a virtual environment because by default all versions of python install packages globally & 
this is *very bad*. Consider you use `sudo` and install some python2.7 version of of a package that OSx uses for some
random important task: you just potentially broke it. Ergo, you can create virtualenvs in one of two ways. You can safely 
install the package `virtualenv` globally using `pip install virtualenv` or use built in python 3 flag to create an env.

> Note, this package will not run on python on any version newer than python 3.6.5. 
> Its a tensorflow error regarding some function call that its not worth taking 
> the time to fix when we need to get tensorflow up to version 2.0 anyway by refactoring
> the existing codebase. I did not write this python code
> however, but ported it from a jupiter notebook and will take some time to go through
> and update tensorflow to work with the breaking changes in version 2. For now, please
> use python 3.6 and I suggest using pyenv which easily allows you have multiple versions
> of python installed at the same time without conflict. 


Before we start installing our python dependencies we will need to install
[caffe](http://caffe.berkeleyvision.org/http://caffe.berkeleyvision.org/installation.html) and those instructions
are a bit rusty, at least for the OSx link provided. Thus, I will walk
you through the rough bits so you don't have issues with missing homebrew packages
and installation issues. 

> As mentioned before, dragons be here, thus 
> be aware that these are only the steps for OSx & will likely work on linux  
> with a bit of tinkering as previously mentioned. I do not provide
> instructions for running this on windows, therefore if you're using windows try following
> the steps on the caffe link above and see if it works. 

First you need to install [homebrew](http://brew.sh), so paste the
following line into your terminal. (On linux, if you decide to use homebrew, you must first install ruby using 
`sudo apt-get install ruby`)

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
$ brew tap brewsci/science
$ brew install hdf5 opencv
``` 

The docs mention setting some compiler flags but aren't needed
for the various installations I've attempted on an array of macs
with various versions of OSx. Lastly, run this:

```bash
$ brew install protobuf boost 
```

By the way, if you have an NVidia card, see the top of the Caffe
link about installing CUDA. Otherwise, neglect it. This script will run
without it, but will use CPU instead of GPU. Although, you may be able
to simply install tensorflow with the GPU version, as mentioned in
the aside about installing this on a jetson nano, so CUDA may get installed
automatically?


### Configuring python virtual environments.

If you already have virtualenv installed you can still use it,  you specify which version of python you want
to use when you create the virtualenv, by using `-p` or `--python` flag, like so:

```bash
$ virtualenv -p python3 venv
```

If you **do not have virtualenv installed**, python3 gives you a crafty builtin way to do this automatically by passing a flag. 
Make sure you are in the root directory of your project and run this command to install a python3 virtual environment.  

```bash
$ python3 -m venv venv
```

Next you need to activate your virtual env:

```bash
$ source venv/bin/activate
```

You will know that your inside your new virtual environment
because the terminal line(s) are prepended with something akin
to this: 

```bash
(venv) $ 
```

Later, when you are done with running your python code,
you can stop the virtual environment by simply running 

```bash
(venv) $ deactivate

# now your terminal no longer shows (venv)
$ ...
```

^ Do not deactivate this environment now, i'm just demonstrating how to 
disable the enviroment later. You must always reactivate the virtual env
before running your python  app. 

## Installing dependencies

In standard python projects all dependencies are installed with pip and saved to a file named `requirements.txt`. 

> This has been a python standard for as long as I can remember.
Anaconda is nice, and I haven't had much time to tinker with it but I can
say that I have deployed many python applications into production 
and written many serverless python apps as well as scripts and its always
been a virtualenv, pip, and a requirements.txt file for dependencies.


Therefore, all you need to before being able to run the script is execute this command in your activated python3 virtual environment.

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


#### Original Author who improved upon the original google deep dream script.
 - [Greg (Grzegorz) Surma](https://gsurma.github.io)
 
#### Author of making this project work for as many people as possible, with documentation, and dependencies, etc.... 
 - [Andrew Hart](https://www.github.com/AndrewJHart)

