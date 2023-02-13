******************
SWaTEval Framework
******************

Setting up the environment
==============================

The following steps describe how to set up and run the project in a dev environment.

**Step 1.** Setup a Python 3.8 environment:

.. note::

    The project was developed using Python 3.8 and there was a known bug when switching to Python 3.10.

.. note::

  This tutorial uses ``conda`` to create a virtual environment and setup the needed dependencies.
  However, you can use any other way to setup a Python 3.8 environment.

Download and install the latest miniconda version

.. code-block::

  wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
  chmod +x ./Miniconda3-latest-Linux-x86_64.sh
  bash ./Miniconda3-latest-Linux-x86_64.sh

Create and activate a virtual environment for Python 3.8

.. code-block::

   conda create -n "scanner" python=3.8
   conda activate scanner

Navigate to the project directory and install the project requirements

.. code-block::

  pip install -r requirements.txt

**Step 2.** Make sure you have Docker and Docker Compose installed by running:

.. note::
    The tests were done using Docker version 20.10.15 and docker-compose version 1.29.2

.. code-block::

  docker --version
  docker-compose --version

**Step 3.** (Optional) Install Docker-DNS gen

.. warning::
    Make sure to properly configure the addresses of your services in the ``config.yaml`` file if you decide to skip
    this step.

To install the Docker DNS server, use the automation script provided in:

.. code-block::

  sudo sh -c "$(curl -fsSL https://raw.githubusercontent.com/jderusse/docker-dns-gen/master/bin/install)"

.. note::
    The DNS gen script creates a DNS server in Docker that exposes the services locally using their internal port
    number and container name.

    Example: You are running a container with name my-demo-webapp which has an http nginx server on port 80 and is exposed
    on 8080. Normally you will access the service using http://localhost:8080, but with Docker-DNS gen you will be able to
    access it also over http://my-demo-webapp.docker:80.

    The default project configuration uses this convention for accessing all of the services running as containers.

    For more info check `this github repositiory <https://github.com/jderusse/docker-dns-gen>`_


**Step 4.** Run the needed services as containers:

.. code-block::

  docker-compose up

.. note::
    Use the :code:`--build` tag to rebuild the containers if you're updating your project branch or version.

Once the images are downloaded and containers are up and running you should have:

.. list-table::
   :widths: 25 60 25 25
   :header-rows: 1

   * - Service
     - Address
     - Internal Port
     - External Port

   * - MongoDB
     - mongo.docker
     - 2017
     - *Not exposed*

   * - Redis
     - redis.docker
     - 6379
     - *Not exposed*

   * - Wackopicko
     - http://wackopicko.docker:80
     - 80
     - 8080

   * - Mongo Express
     - http://mongo-express.docker:8081
     - 8081
     - 8081

   * - Rebrow
     - http://rebrow.docker:5001
     - 5001
     - 8083

   * - RQ-Dashboard
     - http://rq-dashboard.docker:9181
     - 5001
     - 8082

.. note::
    You can skip the following steps and just open the Project in `PyCharm <https://www.jetbrains.com/pycharm/>`_
    and follow the IDE's guide for configuring virtual environment and installing project dependencies.

**Step 5.** (Optional) Install the project dependencies

.. code-block::

  pip install -r requirements.txt


**Step 6.** (Optional) Test if the setup works

First you need to have a Docker image of the Evaluation Framework in your local Docker image repository.
To do this, pull the `Evaluation Framework repositiry <https://www.jetbrains.com/pycharm/>`_ which contains a script that automates the process.
Navigate to the location of the Evaluation Framework and run:

.. code-block::

  bash ./create_image.sh

Navigate back to the location of the scanner and run the main Python script

.. note::
  The default configuration should contain the settings to run the container and start a scan for the evaluation framework

.. code-block::

  python main.py
