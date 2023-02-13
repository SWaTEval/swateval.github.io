************
Architecture
************

The following describes the details of the framework's architecture. Please refer to our paper for a broader overview of the SWaTEval framework.

Scanner's abstraction
=====================

The scanner engine, also referred to as **the scanner**, is composed of multiple concrete modules, which have different or similar tasks, and use
individual approaches to get them done. In order to provide an extendable framework, all of the components implement an abstract
base class called **BaseModule**. As you're going to see later on, this allows the modules to be wrapped in workers and get them running in a
different manner (i.e. in sequential, in parallel, distributed or dockerized), while simultaneously providing different input parameter to each
of them.

.. note::

    The main idea of the **BaseModule** is to provide a standardized interface for the worker wrappers. However, each module can be existing on it's
    own and can be run without being wrapped in a worker wrapper.


.. figure:: img/abstraction.svg
    :align: center

    *BaseModule and it's abstract class derivations*


Two more abstract classes are derived from the **BaseModule**. Those are the **BaseCrawler**, which is an abstraction for the web-crawler part
of the scanner, and the **BaseDetector**, which represents the different detectors that are part of the scanner's state detection pipeline. Both of the
derived abstract classes have their own method, which internally gets invoked when the parent ``run()`` method gets called (i.e. the ``run()`` method
is internally implemented). The suggested abstractions allows further classes to be derived, while simultaneously integrating them in the scanner's pipeline
and making them runnable by a worker wrapper.

BaseModule
----------

.. automodule:: scanner.Base.BaseModule
    :members:

BaseDetecor
-----------

.. automodule:: scanner.Base.BaseDetector
    :members:

Web-Crawler's abstraction
=========================

The web-crawler, also referred to as **the crawler**, is a module responsible for exploring the targeted web-app. The crawler additionally is composed of
two internal modules: **StateNavigator** which selects the current state and navigates to it, and **InteractionHandler** which generates and executes Requests.

BaseCrawler
-----------

.. automodule:: scanner.Base.BaseCrawler
    :members:

BaseInteractionHandler
----------------------

.. automodule:: scanner.Base.BaseInteractionHandler
    :members:


Work Abstraction
================

As mentioned previously, the main idea of the **BaseModule** is to create an interface for the **BaseWork** classes. In this way,
the work classes can wrap each module of the scanner and add additional complexity to the execution logic, without complicating the modules' functionality internally.

Furthermore, the idea behind the work classes is to make different types of module execution possible, as for example a parallel or a sequential run. For this, the **BaseWork** class was implemented, providing the needed interface for future implementations.


.. automodule:: scanner.Base.BaseWork
    :members:
