Azure
-----
Project creation process for Azure migration is also very similar to AWS. We need a storage account container, access key for storage account
and service principal credentials of Azure account. Follow the below steps to create a project for Azure migration.

1. Give a project name and click on Azure logo to set the target cloud as Azure. Then provide the service principal credentials
   of the Azure account and click verify.

   .. image:: images/azure_project-1.png
      :width: 600

2. Now you have to enter a resource group name and select the region. Make sure that provided resource group name is not existing.
   The region you select should be as same as the region of the storage account.

   .. image:: images/azure_project-3.png
      :width: 600

3. In this window you have to enter the storage account details. Storage account name, container and access key and the press the 
   save button to create the project.

   .. image:: images/azure_project-4.png
      :width: 600
