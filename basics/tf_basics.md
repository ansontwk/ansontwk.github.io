---
layout: default
---

# Tensorflow Basics

What is tensorflow?

> Tensorflow is a python library for building machine learning code.

Can I not use tensorflow? What else can I use?

> Tensorflow is not the only option, the other popular python package is PyTorch.


# Installation and Setup

I will only cover the GPU-cuda enabled version.

## Prerequisities 

* a unix based computer (preferably ubuntu; tested on version 20.04)
* a NVIDIA GPU with GPU drivers, CUDA installed (another hell) (optional)
* Conda/miniconda installed

## Installation

Refer to the offical installation page for dependency

https://www.tensorflow.org/install

```sh
conda create -n tensorflow_env python=3.10
```

Press y when prompted. This will create a conda environment called "tensorflow_env" with python version 3.10

```sh
pip install 'tensorflow[and-cuda]'==2.14 #if you have a NVIDIA GPU with CUDA support
```

Note the \' \' bracketing tensorflow\[and-cuda]. This is intentional and required. Adding \' \' treats it as a single unit and parses the whole package.

If you have a GPU, after installation, run:

```sh
python -c "import tensorflow as tf; print(tf.config.list_physical_devices('GPU'))"
```
you will see something like:
```
[PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]
```

This means your installation is all good and ready to go.


## Troubleshooting

For some unknown reason, your tensorflow installation may yell at you about numpy dependency errors. 
If you see something along the lines of:
```
A module that was compiled using NumPy 1.x cannot be run in
NumPy 2.2.1 as it may crash. To support both 1.x and 2.x
versions of NumPy, modules must be compiled with NumPy 2.0.
Some module may need to rebuild instead e.g. with 'pybind11>=2.12'.
```
Downgrade numpy using
```sh
pip uninstall numpy

pip install numpy==1.X.X #X.X is a specified numpy version.
```

[back](../)