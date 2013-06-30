Title: Building numpy with OpenBLAS
Date: 2012-10-12 10:20
Category: Python
Tags: numpy, bento
Author: David Cournapeau
Summary: instructions to build numpy with bento

This is a quick post to show how to build NumPy/SciPy with [OpenBlas](https://github.com/xianyi/OpenBLAS)
on Mac OS X.  OpenBlas is a recently
open-sourced version of Blas/Lapack that is competitive with the proprietary
implementations, without being as hard to build as Atlas.

Note: this is experimental, largely untested, and I would not recommend using
this for anything worthwhile at the moment.

#### Building OpenBlas

After checking out the sources from github, I had the most luck building
openblas with a custom-build clang (I used llvm 3.1). With the apple-provided
clang, I got some errors related to unsupported opcodes (fsubp).

With the correct version of clang, building is a simple matter of running make
(CPU is automatically detected).

#### Building NumPy/SciPy

I have just added a initial suppoer for customizable blas/lapack in the bento
build of NumPy (and scipy). You will need a very recent clone of NumPy git
repo, and a recent bento. The [single file distribution](https://github.com/downloads/cournape/Bento/bentomaker.py)
of bento is the simplest way to make this work:

	./bentomaker.py configure --with-blas-lapack-libdir=$OPENBLAS_DIRECTORY --blas-lapack-type=openblas ..
	./bentomaker.py build -j4 # build with 4 processes in //

Same for SciPy. The code for bento's blas/lapack detection is not very robust
nor well tested, so it will likely not work on most platforms.