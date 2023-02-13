*******************
General information
*******************

The SWaTEval project presents a framework for a modular state aware web scanner that can be extended with additional external scanners or fuzzers to the users needs.
Please consider citing our paper if you use this work for your research:

    Borcherding, A.; Penkov, N.; Giraud, M. and Beyerer, J. (2023). SWaTEval: An Evaluation Framework for Stateful Web Application Testing. In Proceedings of the 9th International Conference on Information Systems Security and Privacy - ICISSP

To be able to recreate and run the components you need to install the following software on your system:

* SWaTEval framework: Python 3.8
* Database: `MongoDB <https://www.mongodb.com/>`_
* Proxy: `MITM Proxy <https://mitmproxy.org/>`_
* Running containers: `Docker <https://www.docker.com/>`_ and `Docker Compose <https://docs.docker.com/compose/>`_

.. note::
    The project was developed using Ubuntu 20.04.4 LTS (Focal Fossa). Any installation steps will assume you are running Ubuntu 20.04
    or later.

.. warning::
    Make sure you're using Python version 3.8 or the project may not run. It should be compatible with any later Python version,
    however while testing on Python 3.10 the `dataclasses-json <https://pypi.org/project/dataclasses-json/>`_ dependency fails to
    serialize lists. There seems to be a dependency bug when using the Typing.List of Python 3.10 which will probably be
    patched in the later versions of the `dataclasses-json <https://pypi.org/project/dataclasses-json/>`_ library.
