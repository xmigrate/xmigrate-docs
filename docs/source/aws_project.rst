AWS
---
There are 2 pre-requisites to do migration of servers to AWS. We need an s3 bucket and access credentials to the AWS account with
full permission to the bucket and permission to create roles and manage compute instances. This is for creating network and compute
resources in the target cloud while migration. Follow the below steps to create a project for AWS migration,

1. Give a project name and click on AWS logo to set the target cloud as AWS. Then provide the access key and secret key of the target 
   cloud account and click verify.

   .. image:: images/aws_project-1.png
      :width: 600

2. Now you have to choose a region from the dropdown menu. Dropdown will be empty if the provided credentials are wrong. Make sure that
   the selected region and the region where the s3 bucket is created is same.

   .. image:: images/aws_project-2.png
      :width: 600

3. Now you have to enter the s3 bucket name and click on save button to finish the project creation process.

   .. image:: images/aws_project-3.png
      :width: 600
