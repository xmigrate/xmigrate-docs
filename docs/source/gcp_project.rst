GCP
---
Project creation process for GCP is also very similar to both AWS and Azure. We need a cloud storage bucket with access key and secret key,
service account credentials for resource creation. Follow the below steps to create a project for GCP migration.

1. Give a project name and click on GCP logo to set the target cloud as GCP. Then provide the service account credential json file, 
   project id and then click verify.

   .. image:: images/gcp_project-1.png
      :width: 600   

2. Now you have to select a region from the dropdown menu. This region should be same as the region of the storage bucket. If dropdown list
   is empty, then either the credntials are wrong or the service account might not have sufficient privileges.

   .. image:: images/gcp_project-2.png
      :width: 600

3. In this screen you have to enter the cloud storage bucket details. Bucket name, access key and secret key and press the save button
   to create the project

   .. image:: images/gcp_project-3.png
      :width: 600