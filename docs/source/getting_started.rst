Getting started
=====
.. _getting_started:
.. _setup:
.. _project:
.. _migration:

Setup
-----

Xmigrate can be run easily using the container image from xmigrate docker registry. We reccomend to
run the application with docker compose file which is provided in the application repo.
Also consider changing the credentials used for mongodb in the `docker-compose.yaml` file and provide
the correct IP address of the server where xmigrate is getting setup in `BASE_URL` field. The IP address 
can be private or public but the servers which you want to migrate using xmigrate should have access to this IP.
Here is an example,

.. code-block:: bash

   BASE_URL: http://24.142.113.45:8000/api



Execute below commands to start xmigrate application

.. code-block:: bash

   git clone https://github.com/xmigrate/xmigrate.git
   cd xmigrate
   docker-compose up -d


Execute the below command to see the logs from xmigrate app

.. code-block:: bash
   
   docker-compose -f app

