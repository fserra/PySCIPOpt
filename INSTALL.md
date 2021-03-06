Building the Python interface
=============================

The SCIP Python interface uses the shared library of the SCIP Optimization Suite.
Therefore you have to run

    make SHARED=true scipoptlib

from the root of the SCIP Optimization directory. This will result in the creation of the directory `<path_to_scipopt/lib>` and the shared library `libscipopt.so`.

From within this directory, please execute the following command:

    python setup.py install

You may use the additional options `--user` or `--prefix=<custom-python-path>`, to build the interface locally.

The interface is written in Cython. If you have Cython installed on your system, the interface will be built from scratch. Otherwise the included pre-built C-code will be used.

TROUBLESHOOTING
===============

The installation routine tries to generate symbolic links to the `scipopt` library as well as to the `src` directory of SCIP. In case of installation problems you should verify the correctness of the links in the directories `lib` and `include`.

Note:
-----

You cannot use the interface module from within this directory. This is because Python will try to import the `pyscipopt` package from the local directory instead of using the installed one.
