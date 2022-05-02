Xmigrate Overview
=================

.. autosummary::
   :toctree: generated

   xmigrate

Xmigrate is designed to support lift and shift migrations of server workloads. Currently, it only supports the migration of Linux servers.
Xmigrate now supports the migration of servers to AWS, Azure, and GCP. Xmigrate works for all kinds of application workload migration like web servers,
DB systems, ERP applications, CRM applications, CMS etc. 

High-level design
-----------------

   .. image:: images/xmigrate_architecture.png
      :width: 800
      :alt: xmigrate architecture diagram

1. Discovery and VM preparation phase triggered with ansible
2. Server and network metadata is sent back to the call back URL
3. Xmigrate trigger the server to start disk cloning 
4. The data is sent to the object storage service in the target cloud directly from the application server
5. Xmigrate download the cloned disk image and convert that to the appropriate format and upload it back to the object storage
6. Network resources will be created based on the blueprint
7. Server will be created after importing the image to the target cloud image service

With this design approach, we don't need any additional servers to be created to store the disk data. All the disks are cloned
directly to the target cloud. 

Cloud and OS compatibility matrix
---------------------------------
Xmigrate currently supports the below operating system versions for each cloud.

 ======== =========== =========== =========== =============== =============== =============== 
     X      Redhat 7    Redhat 8    CentOS 7    Ubuntu 16.04    Ubuntu 18.04    Ubuntu 20.04   
 ======== =========== =========== =========== =============== =============== =============== 
  AWS      ✅           ✅           ✅           ❌               ✅               ❌              
  Azure    ✅           ❌           ✅           ✅               ✅               ✅              
  GCP      ✅           ✅           ❌           ✅               ✅               ✅              
 ======== =========== =========== =========== =============== =============== =============== 
