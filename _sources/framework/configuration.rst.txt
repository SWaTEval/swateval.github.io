*************
Configuration
*************

This section will describe how to configure the scanner using the configuration file ``config.py`` in the root scanner directory.

Sections
========

There are several sections that configure different services and scanner modules. Each of them are described in detail below.

Redis
-----

Holds the address and the credentials needed to establis connection to Redis

.. code-block:: ini

    [redis]
    host = **your redis host**
    port = **your redis port**
    db = **your redis db (usually 0)**

MITM Proxy
----------

Holds the settings for the MITM proxy used by the exteranl scanners

.. code-block:: ini

    [proxy]
    auto_start = ** "no" if you start the proxy manually, "yes" if the scanner should start it**
    scheme = **your proxy scheme (http or https)**
    host = **your proxy host (localhost for local proxy)**
    port = **your proxy port**
    
.. note::
    If the proxy is autostarted the given scheme host and port will be used for proxy setup. If auto start is
    disabled, make sure the data scheme, host and port data match the one of the proxy you are using.

Mongo
-----

The database MongoDB has two sections in the configuration file:

The first one contains the credentials for connection

.. code-block:: ini

    [mongo_db_credentials]
    mongo_host = **mongo host**
    mongo_port = **mongo port (default usually is 27017)**
    username= **leave empty if no user is needed for authentication**
    password= **leave empty if no user is needed for authentication**


The second one contains the names for the databases where data should be read from and written to:

.. code-block:: ini

    [mongo_db_names]
    interactions = ** "interactions" or give a custom name**
    states = ** "states" or give a custom name**
    endpoints = ** "endpoints" or give a custom name**
    endpoint_clustering = ** "endpoint_clustering" or give a custom name**
    interaction_clustering = ** "interaction_clustering" or give a custom name**


Vulnarable Web App
------------------

Contains the VWA data 

.. warning::

    **Not fully implemented or properly used feature**. 
    
    Currently this section is used to extract the address of the target app, when the scanner is running 
    in dev mode (i.e. in IDE and not in the backend server). The initial idea was to auto start the vulnarable 
    web app as a docker contai
    ner and redeploy it, when a reset is needed. This approach was replaced with a 
    simpler one, but the idea remains possible for future implemntations. This is why this section is not yet removed.

.. code-block:: ini

    [vulnerable_web_app]
    docker_image = **name of the docker image (local or from the hub)**
    container_name = **name of the container where the image will be deployed**
    container_port = **port of app**
    app_scheme = **depends on the server configuration in the image (http or https)**

Workers
-------

Here the workers are selected

.. code-block:: ini

    [workers]
    execution_type = *sequential, parallel-rq or parallel-threaded*
    crawler_module = **the full python module path to the module's file**
    crawler_class = **the modules class name**

    endpoint_detector_module = **the full python module path to the module's file**
    endpoint_detector_class = **the modules class name**

    endpoint_cleaner_module = **the full python module path to the module's file**
    endpoint_cleaner_class = **the modules class name**

    state_detector_module = **the full python module path to the module's file**
    state_detector_class = **the modules class name**

    state_collapser_module = **the full python module path to the module's file**
    state_collapser_class = **the modules class name**

Worker Settings
---------------

There are multiple sections that configure the different workers:

State Navigator
^^^^^^^^^^^^^^^

.. code-block:: ini

    [state_navigator]
    max_revisits = **how many times the state navigator should revisit an endpoint in a state**


Endpoint Detector
^^^^^^^^^^^^^^^^^

.. code-block:: ini

    [endpoint_detector]
    restrict_host = ** "yes" or "no" - visit only endpoints on the current host**
    allow_all_visit = **allow every endpoint found to be visited indepndet if it's duplicate**
    mark_always_clean = **mark every endpoint as clean (i.e. ignore clustering)**

Endpoint Cleaner 
^^^^^^^^^^^^^^^^

.. code-block:: ini

    [endpoint_cleaner]
    distance_type = **check the Distance class in the Utilities for all possible distance or leave empty to use the Hash2Vec method**
    delete_dirty = ** "yes" if the duplicate endpoints should be deleted and "no" if they should be only flagged for skipping **


State Change Detector
^^^^^^^^^^^^^^^^^^^^^

.. code-block:: ini

    [state_change_detector]
    distance_type = **check the Distance class in the Utilities for all possible distance or leave empty to use the Hash2Vec method**


State Collapser
^^^^^^^^^^^^^^^

.. code-block:: ini
    
    [state_collapser]
    distance_type = **check the Distance class in the Utilities for all possible distance or leave empty to use the Hash2Vec method**
    delete_collapsed = ** "yes" if the duplicate states will be deleted and "no" if there should be only flagged as collapsed **
