*****************************
Evaluation Notebooks
*****************************

There are Jupyter notebooks provided in the `SWATEval framework repositiory <https://github.com/SWaTEval/framework>`_
in the ``notebooks`` folder.


Apps Evaluation Notebook 
==========================

This notebooks can be used to generate evaluation data from the data provided in:

.. code-block::

   Yandrapally, R., Stocco, A., and Mesbah, A. (2020). 
   Near-duplicate detection in web app model inference. 
   In ACM/IEEE 42nd international conference on software engineering, pages 186–197.

* Link to the paper: https://dl.acm.org/doi/pdf/10.1145/3377811.3380416
* Link to the paper repo: https://github.com/NDStudyICSE2019/NDStudy
* Dataset link: https://zenodo.org/record/3385377#.Y3SjkL7MKV4

The provided dataset has a different representation of the web content. 
The notebook converts the representation to the one used in the SWaTEval framework.
It also applies the method described in the SWaTEval paper and creates output data for comparison.


Literature vs Ours Comparison Notebook
========================================

This notebook compares the data from the literature with the data from our framework.

.. note::

    To run this notebook you need the data from the `evaluation data repositiory <https://github.com/SWaTEval/evaluation-data>`_
    In the ``raw`` folder there is data from the SWaTEval target and preprocessed data from the mentioned literature.

    Alternatively, you can generate the evaluation data from the literature using the ``Apps Evaluation`` notebook and respectively
    use new data from the SWaTEval target by running the SWaTEval framework on the SWATEval target and extracting the data generated
    from the run. 



Module Evaluation Data Notebook
========================================

This notebook evaluates the different module configuration proposed in the SWaTEval framework.

.. note::

    There exists already generated data for all SWaTEval framework configuration which is available in the `evaluation data repositiory <https://github.com/SWaTEval/evaluation-data>`_.

    * The ``Basic ED Experiments`` folder contains all runs which use the **BasicEndpointDetector**
    * The ``Clustering Based ED Experiments`` folder contains all runs which use the **ClusteringBasedEndpointDetector**

To evaluate the modules all framework configurations were applied and runned multiple times.
There are helper scripts that automate this process. They can be found in the ``helpers`` folder
of SWaTEval framework.

* The ``experiment_creator.py`` script creates the configurations for all runs.
* The ``experiment_runner.py`` script runs a single configuration.
* The ``experiment_coordinator.py`` script runs multiple configuration multiple times using predefined seeds for the random number generator.
It also exports the generated data grom MongoDB and saves them in ``experiments`` folder. 

.. note::

    The ``experiment_coordinator.py`` script automatically executes the ``experiment_creator.py`` and ``experiment_runner.py`` scripts.
    It also clears the database after each run using the ``clear_mongo_db_whole.py`` script which, as the name sugests, clears the 
    whole content of MongoDB.