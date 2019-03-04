**Docker for Datascience**
--------------------------

Improving your data science workflow using Docker containers 
=============================================================

For a data scientist, running a container that is already equipped with the libraries and tools needed for a particular analysis eliminates the need to spend hours debugging packages across different environments or configuring custom environments.

But why Set Up a Data Science Environment in a Container?

- One reason is speed. Docker containers allow a Jupyter or RStudio session to launch in minutes, not hours. We also want them to have that fast user experience while still working in a governed, central architecture (rather than on their local machines). 

- Containerization benefits both data science and IT/technical operations teams. In the DataScience.com Platform, for instance, we allow IT to configure environments with different languages, libraries, and settings in an admin dashboard and make those images available in the dropdown menu when a data scientist launches a session. These environments can be selected for any run, session, scheduled job, or API. (Or you don’t have to configure anything at all. We provide plenty of standard environment templates to choose from.)

- Ultimately, containers solve a lot of common problems associated with doing data science work at the enterprise level. They take the pressure off of IT to produce custom environments for every analysis, standardize how data scientists work, and ensure that old code doesn’t stop running because of environment changes. To start using containers and our library of curated images to do collaborative data science work, request a demo of our platform today.

- Configuring a data science environment can be a pain. Dealing with inconsistent package versions, having to dive through obscure error messages, and having to wait hours for packages to compile can be frustrating. This makes it hard to get started with data science in the first place, and is a completely arbitrary barrier to entry.

Thanks to the rich ecosystem, there are already several readily available images for the common components in data science pipelines. Here are some Docker images to help you quickly spin up your own data science pipeline:

- `MySQL <https://hub.docker.com/_/mysql/>`_
- `Postgres <https://hub.docker.com/_/postgres/>`_
- `Redmine <https://hub.docker.com/_/redmine/>`_
- `MongoDB <https://hub.docker.com/_/mongo/>`_
- `Hadoop <https://hub.docker.com/r/sequenceiq/hadoop-docker/>`_
- `Spark <https://hub.docker.com/r/sequenceiq/spark/>`_
- `Zookeeper <https://hub.docker.com/r/wurstmeister/zookeeper/>`_
- `Kafka <https://github.com/spotify/docker-kafka>`_
- `Cassandra <https://hub.docker.com/_/cassandra/>`_
- `Storm <https://github.com/wurstmeister/storm-docker>`_
- `Flink <https://github.com/apache/flink/tree/master/flink-contrib/docker-flink>`_
- `R <https://github.com/rocker-org/rocker>`_

Motivation: Say you want to play around with some cool data science libraries in Python or R but what you don’t want to do is spend hours on installing Python or R, working out what libraries you need, installing each and every one and then messing around with the tedium of getting things to work just right on your version of Linux/Windows/OSX/OS9 — well this is where Docker comes to the rescue! With Docker we can get a Jupyter ‘Data Science’ notebook stack up and running in no time at all. Let’s get started! We will see few examples of thse in the following sections...

.. Note::

	The above code can be found in this `github <https://github.com/upendrak/jupyternotebook_docker>`_

1. Launch a Jupyter notebook conatiner

Docker allows us to run a ‘ready to go’ Jupyter data science stack in what’s known as a container:

1.1 Create a `docker-compose.yml` file

.. code-block:: bash

	$ mkdir jn && cd jn

.. code-block:: bash
	
	version: '2'

	services:
	  datascience-notebook:
	    image: jupyter/datascience-notebook
	    volumes:
	      - .:/data
	    ports:
	      - 8888:8888
	    container_name:   datascience-notebook-container

.. Note::

	The ``jupyter/datascience-notebook`` image can be found on dockerhub

|jn_ss|

1.2 Run container using docker-compose file

.. code-block:: bash

	$ docker-compose up
	Creating datascience-notebook-container ... 
	Creating datascience-notebook-container ... done
	Attaching to datascience-notebook-container
	datascience-notebook-container | Execute the command: jupyter notebook
	datascience-notebook-container | [I 08:44:31.312 NotebookApp] Writing notebook server cookie secret to /home/jovyan/.local/share/jupyter/runtime/notebook_cookie_secret
	datascience-notebook-container | [W 08:44:31.332 NotebookApp] WARNING: The notebook server is listening on all IP addresses and not using encryption. This is not 	recommended.
	datascience-notebook-container | [I 08:44:31.370 NotebookApp] JupyterLab alpha preview extension loaded from /opt/conda/lib/python3.6/site-packages/jupyterlab
	datascience-notebook-container | JupyterLab v0.27.0
	datascience-notebook-container | Known labextensions:
	datascience-notebook-container | [I 08:44:31.373 NotebookApp] Running the core application with no additional extensions or settings
	datascience-notebook-container | [I 08:44:31.379 NotebookApp] Serving notebooks from local directory: /home/jovyan
	datascience-notebook-container | [I 08:44:31.379 NotebookApp] 0 active kernels 
	datascience-notebook-container | [I 08:44:31.379 NotebookApp] The Jupyter Notebook is running at: http://[all ip addresses on your 	system]:8888/?token=dfb50de6c1da091fd62336ac52cdb88de5fe339eb0faf478
	datascience-notebook-container | [I 08:44:31.379 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
	datascience-notebook-container | [C 08:44:31.380 NotebookApp] 
	datascience-notebook-container |     
	datascience-notebook-container |     Copy/paste this URL into your browser when you connect for the first time,
	datascience-notebook-container |     to login with a token:
	datascience-notebook-container |         http://localhost:8888/?token=dfb50de6c1da091fd62336ac52cdb88de5fe339eb0faf478

The last line is a URL that we need to copy and paste into our browser to access our new Jupyter stack:

.. code-block:: bash

	http://localhost:8888/?token=dfb50de6c1da091fd62336ac52cdb88de5fe339eb0faf478

.. warning::

	Do not copy and paste the above URL in your browser as this URL is specific to my environment.

Once you’ve done that you should be greeted by your very own containerised Jupyter service!

|jn_login|

To create your first notebook, drill into the work directory and then click on the ‘New’ button on the right hand side and choose ‘Python 3’ to create a new Python 3 based Notebook. 

|jn_login2|

Now you can write your python code. Here is an example

|jn_login3|

|jn_login3.5|

To shut down the container once you’re done working, simply hit Ctrl-C in the terminal/command prompt. Your work will all be saved on your actual machine in the path we set in our Docker compose file. And there you have it — a quick and easy way to start using Jupyter notebooks with the magic of Docker.

2. Launch a R-Studio container

Next, we will see a Docker image from Rocker which will allow us to run RStudio inside the container and has many useful R packages already installed.

|rstudio_ss|

.. code-block:: bash

	$ docker run --rm -d -p 8787:8787 rocker/rstudio:3.4.3

.. Note:: 
	
	 ``–rm`` ensures that when we quit the container, the container is deleted. If we did not do this, everytime we run a container, a version of it will be saved to our local computer. This can lead to the eventual wastage of a lot of disk space until we manually remove these containers. 

The command above will lead RStudio-Server to launch invisibly. To connect to it, open a browser and enter http://localhost:8787, or <ipaddress>:8787 on cloud 

|rstudio_login2|

Enter ``rstudio`` as username and password. Finally Rstudio shows up and you can run your R command from here

|rstudio_login|

3. Machine learning using Docker

In this simple example we’ll take a sample dataset of fruits metrics (like size, weight, texture) labelled apples and oranges. Then we can predict the fruit given a new set of fruit metrics using scikit-learn’s decision tree

You can find the above code in this `github repo <https://github.com/upendrak/scikit_tree_docker>`_ 

1. Create a directory that consists of all the files

.. code-block:: bash

	$ mkdir scikit_docker && cd scikit_docker

2. Create ``requirements.txt`` file — Contains python modules and has nothing to do with Docker inside the folder - ``scikit_docker``.

.. code-block:: bash

	numpy
	scipy
	scikit-learn

3. Create a file called ``app.py`` inside the folder — ``scikit_docker``

.. code-block:: bash

	from sklearn import tree
	#DataSet
	#[size,weight,texture]
	X = [[181, 80, 44], [177, 70, 43], [160, 60, 38], [154, 54, 37],[166, 65, 40], [190, 90, 47], [175, 64, 39], [177, 70, 40], [159, 55, 37], [171, 75, 42], [181, 85, 43]]

	Y = ['apple', 'apple', 'orange', 'orange', 'apple', 'apple', 'orange', 'orange', 'orange', 'apple', 'apple']

	#classifier - DecisionTreeClassifier
	clf_tree = tree.DecisionTreeClassifier();
	clf_tree = clf_tree.fit(X,Y);

	#test_data
	test_data = [[190,70,42],[172,64,39],[182,80,42]];

	#prediction
	prediction_tree = clf_tree.predict(test_data);

	# Write output to a file
	with open("output.txt", 'w') as fh_out:
		fh_out.write("Prediction of DecisionTreeClassifier:")
		fh_out.write(str(prediction_tree))

4. Create a Dockerfile that contains all the instructions for building a Docker image inside the project directory

.. code-block:: bash

	# Use an official Python runtime as a parent image
	FROM python:3.6-slim
	MAINTAINER Upendra Devisetty <upendra@cyverse.org>
	LABEL Description "This Dockerfile is used to build a scikit-learn’s decision tree image"

	# Set the working directory to /app
	WORKDIR /app

	# Copy the current directory contents into the container at /app
	ADD . /app

	# Install any needed packages specified in requirements.txt
	RUN pip install -r requirements.txt

	# Define environment variable
	ENV NAME World

	# Run app.py when the container launches
	CMD ["python", "app.py"]

5. Create a Docker compose YAML file

.. code-block:: bash

	version: '2'
	services:
	    datasci:
	        build: .
	        volumes:
	            - .:/app

5. Now Build and Run the Docker image using `docker-compose up` command to predict the fruit given a new set of fruit metrics

.. code-block:: bash

	$ docker-compose up 
	Building datasci
	Step 1/8 : FROM python:3.6-slim
	 ---> dc41c0491c65
	Step 2/8 : MAINTAINER Upendra Devisetty <upendra@cyverse.org>
	 ---> Running in 95a4da823100
	 ---> 7c4d5b78bb0a
	Removing intermediate container 95a4da823100
	Step 3/8 : LABEL Description "This Dockerfile is used to build a scikit-learn’s decision tree image"
	 ---> Running in e8000ae57a7d
	 ---> d872e29971e3
	Removing intermediate container e8000ae57a7d
	Step 4/8 : WORKDIR /app
	 ---> 083eb3e4fb16
	Removing intermediate container c965871286f9
	Step 5/8 : ADD . /app
	 ---> 82b1dbdbe759
	Step 6/8 : RUN pip install -r requirements.txt
	 ---> Running in 3c82f7d5dd95
	Collecting numpy (from -r requirements.txt (line 1))
	  Downloading numpy-1.14.0-cp36-cp36m-manylinux1_x86_64.whl (17.2MB)
	Collecting scipy (from -r requirements.txt (line 2))
	  Downloading scipy-1.0.0-cp36-cp36m-manylinux1_x86_64.whl (50.0MB)
	Collecting scikit-learn (from -r requirements.txt (line 3))
	  Downloading scikit_learn-0.19.1-cp36-cp36m-manylinux1_x86_64.whl (12.4MB)
	Installing collected packages: numpy, scipy, scikit-learn
	Successfully installed numpy-1.14.0 scikit-learn-0.19.1 scipy-1.0.0
	 ---> 3d402c23203f
	Removing intermediate container 3c82f7d5dd95
	Step 7/8 : ENV NAME World
	 ---> Running in d0468b521e81
	 ---> 9cd31e8e7c95
	Removing intermediate container d0468b521e81
	Step 8/8 : CMD python app.py
	 ---> Running in 051bd2235697
	 ---> 36bb4c3d9183
	Removing intermediate container 051bd2235697
	Successfully built 36bb4c3d9183
	Successfully tagged scikitdocker_datasci:latest
	WARNING: Image for service datasci was built because it did not already exist. To rebuild this image you must use `docker-compose build` or `docker-compose up --build`.
	Creating scikitdocker_datasci_1 ... 
	Creating scikitdocker_datasci_1 ... done
	Attaching to scikitdocker_datasci_1
	scikitdocker_datasci_1 exited with code 0

Use ``docker-compose rm`` to remove the container after docker-compose finish running

.. code-block:: bash

	docker-compose rm 
	Going to remove scikitdocker_datasci_1
	Are you sure? [yN] y
	Removing scikitdocker_datasci_1 ... done

You will find the ouput file in the ``scikit_docker`` folder with the following contents

Repo2docker


jupyter-repo2docker https://github.com/upendrak/keras_wine
