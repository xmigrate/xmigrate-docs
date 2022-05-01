Xmigrate Architecture
=====================

.. autosummary::
   :toctree: generated

   xmigrate

Xmigrate is designed to support lift and shift migrations of server workloads. Currently it only supports migration of Linux servers.
Xmigrate now supports migration of servers to AWS, Azure and GCP. Xmigrate works for all kind of application workload migration like web server,
DB systems, ERP applications, CRM etc. 

High level design
-----------------

   .. image:: images/xmigrate_architecture.png
      :width: 800
      :alt: xmigrate architecture diagram

1. Discovery and VM preparation phase triggered with ansible
2. Server and network metadata is send back to the call back url
3. Xmigrate trigger the server to start disk cloning 
4. The data is send to the object storage service in target cloud directly from the application server
5. Xmigrate download the cloned disk image and convert that to appropriate format and upload it back to the object storage
6. Network resources will be created based on the blueprint
7. Server will be created after importing the image to the target cloud image service

With this design approach we don't need any additional server to be created to store the disk data. All the disks are cloned
directly to the target cloud. 