Xmigrate Overview
=================

.. autosummary::
   :toctree: generated

   xmigrate

Xmigrate is designed to support lift and shift migrations of server workloads. As of now Xmigrate support extends to the migration of servers to AWS, Azure, and GCP clouds. Currently this migration support is limited to Linux servers. Xmigrate works for all kinds of application workload migrations like web servers, DB systems, ERP applications, CRM applications, CMS etc. 

High-level design
-----------------

   .. image:: images/xmigrate_architecture.png
      :width: 800
      :alt: xmigrate architecture diagram

1. Discovery phase is triggered with Ansible.
2. Server and Network metadata is sent back to the call back URL.
3. Xmigrate triggers the server to create the Network resources as defined in the blueprint.
4. Xmigrate triggers the server to prepare the target VM for migration.
5. Xmigrate triggers the server to start Disk cloning.
6. The disk data is sent to the object storage service in the target cloud directly from the application server.
7. Xmigrate downloads the cloned disk image and converts it to the appropriate format and uploads it back to the object storage.
8. Server will be created after importing the image to the target cloud image service.

With this design approach, we don't need any additional servers to be created to store the disk data. All the disks are cloned
directly to the target cloud. 

Cloud and OS compatibility matrix
---------------------------------
Xmigrate currently supports the below operating system versions for each cloud.

 ======== =========== =========== =========== =============== =============== =============== 
     X      Redhat 7    Redhat 8    CentOS 7    Ubuntu 16.04    Ubuntu 18.04    Ubuntu 20.04   
 ======== =========== =========== =========== =============== =============== =============== 
  AWS      ✅           ✅           ✅           ✅               ✅               ✅              
  Azure    ✅           ✅           ✅           ✅               ✅               ✅              
  GCP      ✅           ✅           ✅           ✅               ✅               ✅              
 ======== =========== =========== =========== =============== =============== =============== 
