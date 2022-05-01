Getting started
===============
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

Project
-------

Once the application is up and running the next step is to signup. After signup login to the application using the credentials.
Now, we have to create a project to start the migration. We define the target cloud in this process. 
Below are the detailed steps with screenshots to create project for each cloud provider,

AWS
^^^
There are 2 pre-requisites to do migration of servers to AWS. We need an s3 bucket and access credentials to the AWS account with
full permission to the bucket and permission to create roles and manage compute instances. This is for creating network and compute
resources in the target cloud while migration. Follow the below steps to create a project for AWS migration,

1. Give a project name and click on AWS logo to set the target cloud as AWS. Then provide the access key and secret key of the target 
   cloud account and click verify.

   .. image:: images/aws_project-1.png
      :width: 600
      :alt: xmigrate aws project creation

2. Now you have to choose a region from the dropdown menu. Dropdown will be empty if the provided credentials are wrong. Make sure that
   the selected region and the region where the s3 bucket is created is same.

   .. image:: images/aws_project-2.png
      :width: 600
      :alt: xmigrate aws project creation

3. Now you have to enter the s3 bucket name and click on save button to finish the project creation process.

   .. image:: images/aws_project-3.png
      :width: 600
      :alt: xmigrate aws project creation

Azure
^^^^^
Project creation process for Azure migration is also very similar to AWS. We need a storage account container, access key for storage account
and service principal credentials of Azure account. Follow the below steps to create a project for Azure migration.

1. Give a project name and click on Azure logo to set the target cloud as Azure. Then provide the service principal credentials
   of the Azure account and click verify.

   .. image:: images/azure_project-1.png
      :width: 600
      :alt: xmigrate azure project creation

2. Now you have to enter a resource group name and select the region. Make sure that provided resource group name is not existing.
   The region you select should be as same as the region of the storage account.

   .. image:: images/azure_project-3.png
      :width: 600
      :alt: xmigrate azure project creation

3. In this window you have to enter the storage account details. Storage account name, container and access key and the press the 
   save button to create the project.

   .. image:: images/azure_project-4.png
      :width: 600
      :alt: xmigrate azure project creation

GCP
^^^
Project creation process for GCP is also very similar to both AWS and Azure. We need a cloud storage bucket with access key and secret key,
service account credentials for resource creation. Follow the below steps to create a project for GCP migration.

1. Give a project name and click on GCP logo to set the target cloud as GCP. Then provide the service account credential json file, 
   project id and then click verify.

   .. image:: images/gcp_project-1.png
      :width: 600   
      :alt: xmigrate gcp project creation

2. Now you have to select a region from the dropdown menu. This region should be same as the region of the storage bucket. If dropdown list
   is empty, then either the credntials are wrong or the service account might not have sufficient privileges.

   .. image:: images/gcp_project-2.png
      :width: 600
      :alt: xmigrate gcp project creation

3. In this screen you have to enter the cloud storage bucket details. Bucket name, access key and secret key and press the save button
   to create the project

   .. image:: images/gcp_project-3.png
      :width: 600
      :alt: xmigrate gcp project creation


Migration
---------
We can start migrating servers after creating the project. But before getting into the migration process with xmigrate, please 
ensure the following points

   1. Make sure /etc/fstab contains the mountpoints with block-id rather than the device label.
   2. Make sure discard flag is added in the /etc/fstab mountpoint entries
   3. Esure 5th flags of /etc/fstab mountpoint entries are 1 and 6th flag for the boot volume is 1
   4. Ensure the VM is using the latest or the supported version of linux kernels by the target cloud provider
   5. Convert the boot partition to MBR if yo have GPT partition scheme and you want to migrate to AWS cloud

While the point number 5 is only applicable for AWS migration, all the other points are important for all 3 cloud provides.

Migration process involves 5 main steps,
   1. Discovery and preparation
   2. Blueprint creation
   3. Landing zone creation
   4. Disk cloning
   5. Disk convert
   6. Server build in target cloud

Discovery and preparation
^^^^^^^^^^^^^^^^^^^^^^^^^
In this phase we gather informations about the server and the network. We also install aws cli or azcopy or gsutil based on
the target cloud provider. This is to copy the disk data to the target cloud object storage service.
We can provide the IP's or hostnames in the `server ips` field. It also need the `username` and the `password` with sudo privilege.
The same user credentials should be common for all the servers.

   .. image:: images/discovery-1.png
      :width: 600   
      :alt: xmigrate discovery phase

Once the discovery is finished, the `Go to Blueprint` button will be enabled and we should click on that to go to the blueprint creation
page.

   .. image:: images/discovery-2.png
      :width: 600   
      :alt: xmigrate discovery phase

      
Blueprint creation
^^^^^^^^^^^^^^^^^^
In the blueprint creation process we design the landing zone(network and subnet CIDR's) and decide the machine type of each servers.
Details of each servers is displayed in the first table in the blueprint page.

   .. image:: images/discovery-4.png
      :width: 600   
      :alt: xmigrate discovered hosts

First we need to create the network as seen in the below screenshot.

   .. image:: images/blueprint-1.png
      :width: 600   
      :alt: xmigrate blueprint network creation
   
Then we need to create a subnet as seen in the below screenshot. We have to pass the subnet CIDR and select if the network is public
or private. 

   .. image:: images/blueprint-2.png
      :width: 600   
      :alt: xmigrate blueprint network creation

Now we will get all the discovered server's mapped to the first subnet which we just created. Next step is to select a machine type 
for the seerver to be creatd in the target cloud and save the blueprint.

   .. image:: images/blueprint-3.png
      :width: 600   
      :alt: xmigrate blueprint save

Landing zone creation
^^^^^^^^^^^^^^^^^^^^^
Once we create and save the blueprint we can create the necessary network resources for the migration by clicking on the build network
button.

   .. image:: images/blueprint-4.png
      :width: 600   
      :alt: xmigrate build network

Disk cloning
^^^^^^^^^^^^
Clone button will get enabled after the network creation is completed. We can start cloning by clicking the clone button.

   .. image:: images/blueprint-clone.png
      :width: 600   
      :alt: xmigrate disk clone

Disk data will be cloned directly to the target cloud's object storage.

Disk convert
^^^^^^^^^^^^
We clone the disk image in raw format to the object storage. Each cloud provider need disk image to be in certain format.
We convert the disk image into required format in this step. Click on the convert button as it get enabled after cloning.

   .. image:: images/blueprint-convert.png
      :width: 600   
      :alt: xmigrate disk convert

Server build in target cloud
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
As the disk conversion get completes we can click on the build button to start the server build.

   .. image:: images/blueprint-build.png
      :width: 600   
      :alt: xmigrate build server

Status will now get changed to 100 when the server build get completed.

   .. image:: images/blueprint-complete.png
      :width: 600   
      :alt: xmigrate build complete
