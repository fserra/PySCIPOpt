How to build a model using python-scip
======================================

There are several examples provided in the `tests` folder. These display some functionality of the interface and can serve as an entry point for writing more complex code. The following steps are always required when using the interface:

1) It is necessary to import python-scip in your code. This is achieved by including the line

    from pyscipopt import Model

2) Create a solver instance.

    model = Model("Example")    # the name is optional

This is equivalent to calling `SCIPcreate(&scip); SCIPcreateProbBasic(scip, "Example")` in C.

3)  Access the methods in the `scip.pyx` file using the solver/model instance `model`, e.g.:

    x = model.addVar("x")
    y = model.addVar("y", vtype="INTEGER")
    model.setObjective(x + y)
    model.addCons(2*x - y*y >= 0)
    model.optimize()


Writing new plugins
===================

The Python interface can be used to define custom plugins to extend the functionality of SCIP. You may write a pricer, heuristic or even constraint handler using pure Python code and SCIP can call their methods using the callback system. Every available plugin has a base class that you need to extend, overwriting the predefined but empty callbacks. Please see `test_pricer.py` and `test_heur.py` for two simple examples.


How to extend the interface
===========================

The interface python-scip already provides many of the SCIP callable library methods. You may also extend python-scip to increase the functionality of this interface.The following will provide some directions on how this can be achieved:

The two most important files in PySCIPOpt are the `scip.pxd` and `scip.pyx`. These two files specify the public functions of SCIP that can be accessed from your python code.

To make PySCIPOpt aware of the public functions you would like to access, you must add them to `scip.pxd`. There are two things that must be done in order to properly add the functions:

   1) Ensure any `enum`s, `struct`s or SCIP variable types are included in `scip.pxd`
   
   2) Add the prototype of the public function you wish to access to `scip.pxd`

After following the previous two steps, it is then possible to create functions in python that reference the SCIP public functions included in `scip.pxd`. This is achieved by modifying the `scip.pyx` file to add the functionality you require.
