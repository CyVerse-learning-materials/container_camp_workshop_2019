**NVIDIA-Docker**
=================

Background
~~~~~~~~~~

NVIDIA is one of the leading makers of graphic processing units (GPU). GPU were established as a means of handling graphics processing operations for video cards, but have been greatly expanded for use in generalized computing applications. GPU are used for various applications in Machine Learning, image processing, and matrix-based linear algebras.

NVIDIA Docker
~~~~~~~~~~~~~

|NVIDIA-docker-diagram|

NVIDIA have created their own set of Docker containers for running on CPU-GPU enabled systems.

`NVIDIA-Docker <xhttps://github.com/NVIDIA/nvidia-docker>`_ runs atop the NVIDIA graphics drivers on the host system, the NVIDIA drivers are imported to the container at runtime.

`NVIDIA Docker Hub <https://hub.docker.com/u/nvidia>`_ hosts numerous NVIDIA Docker containers, from which you can build your own images.

NVIDIA GPU Cloud
~~~~~~~~~~~~~~~~

`NVIDIA GPU Cloud <https://ngc.nvidia.com>`_ hosts numerous containers for HPC and Cloud applications. You must register an account with them (free) to access these. 

Running NVIDIA Docker with Singularity
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can run NVIDIA Docker on HPC by using Singularity, but it requires a few steps, including authentication to NVIDIA GPU cloud.

`NVIDIA to Singularity Official YouTube demo <https://youtu.be/iOLVqqHQsBU>`_

.. |NVIDIA-docker-diagram| image:: 5b208976-b632-11e5-8406-38d379ec46aa.png 
                           :target: https://cloud.githubusercontent.com/assets/3028125/12213714/5b208976-b632-11e5-8406-38d379ec46aa.png 
                           :width: 800
    
