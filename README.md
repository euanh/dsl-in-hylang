# DSL in Lisp...in Hy, on Python

This tutorial is based on a [video](https://www.youtube.com/watch?v=5FlHq_iiDW0) by Rainer Joswig.  In the video, he writes a Lisp solution to an [article](https://www.martinfowler.com/articles/languageWorkbench.html) about Domain Specific Languages by Martin Fowler.  Rainer used Common Lisp - specifically [LispWorks](http://www.lispworks.com), who are our neighbours across the road in the St John's Innovation Centre.  We will translate his solution into [Hy](http://hylang.org), a Lisp which transpiles to Python.

The main points of interest are:
 * [Hy syntax](http://docs.hylang.org/en/stable/tutorial.html#hy-is-a-lisp-flavored-python)
 * [Multiple dispatch (multimethods)](https://en.wikipedia.org/wiki/Multiple_dispatch)
 * [Macros](http://docs.hylang.org/en/stable/tutorial.html#macros)

## Setting up

The tutorial is [Jupyter](http://jupyter.org) notebook.  I recommend installing Hy and Jupyter in a [virtualenv](https://docs.python.org/3/library/venv.html) - I used a Python 3 one.

First, create and activate the virtualenv.   These commands will create the virtualenv in a subdirectory of your home directory called `hylang`, but you can create it wherever you like.

    bash-4.4$ python3 -m venv ~/hylang
    bash-4.4$ source ~/hylang/bin/activate

Your prompt will now show your virtualenv's name.   It may be different if you created the virtualenv somewhere else.  

Now install Hy and Jupyter:

    (hylang) bash-4.4$ pip3 install hy jupyter 

Finally install Calysto Hy, which lets you run Hy code in a Jupyter notebook.    When I tried, Calysto Hy was not available in pip so I had to install it from its [GitHub repository](https://github.com/Calysto/calysto_hy):

    (hylang) bash-4.4$ pip3 install git+https://github.com/Calysto/calysto_hy.git
    (hylang) bash-4.4$ python3 -m calysto_hy install --sys-prefix

## Running the notebook

Make sure that you are in the directory containing `DSL in Lisp.ipynb` and start Jupyter:

    (hylang) bash-4.4$ jupyter notebook 'DSL in Lisp.ipynb'

A browser window will open and Jupyter will run the notebook.

## Getting started with Hy

The [official documentation for Hy](http://docs.hylang.org/en/stable/) is very good.   The Calysto Hy repository also contains quite a nice [introductory notebook for Hy](https://github.com/Calysto/calysto_hy/blob/master/notebooks/Tutorial.ipynb).

Hy provides a toplevel, called `hy`, in which you can evaluate code interactively.   Make sure your Hylang virtualenv is activated before running it:

    (hylang) bash-4.4$ hy
    hy 0.13.0 using CPython(default) 3.6.3 on Linux
    => (print "Hello world")
    Hello world
    => (exit)

Hy is transpiled to Python.    The `hy2py` utility can show you the Python code which will be generated for a Hy program.

    (hylang) bash-4.4$ cat hello.hy 
    (print "Hello world" 1 2 3)
    (hylang) bash-4.4$ hy2py hello.hy 
    print('Hello world', 1, 2, 3)

