Miscellaneous
=============

.. autosummary::
   :toctree: generated

   xmigrate

AWS
---
AWS migrations only work if the disk partition scheme of boot volume is in MBR. So we need to manualy convert the boot volume 
partition before starting the migration process. For the conversion, we use a utility called gdisk.
Follow the below steps to convert GPT boot volumes to MBR.

1. Execute below command to check the partition scheme of the disk
   
   .. code-block:: bash
      
      gdisk -l /dev/sda

2. Execute below command to start converting the disk from MBR to GPT
   
   .. code-block:: bash
      
      gdisk /dev/sda

3. After entering the interactive console of gdisk, enter `r` to select `Recovery and transformation options` then press 
   `g` to `Convert GPT into MBR and exit` then `Print the MBR partition table` by pressing `p` and press `w` to write the 
   partition table and exit.

4. Reboot the server


