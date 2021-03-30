# DataNode-contributing-Limited-Specified-storage-to-Cluster-Hadoop-

First of all we will check our initial storage allocated by DataNode to NameNode

       
       -> WebUI(IP:50070)
           50070 port number on which NameNode works by default
           







Then we will add a storage device to the DataNode





To check, we can use a command to list all the disk attached to that device:

       command: #fdisk -l
  





After allocating the storage device we will have to make that disk ready to use:
      
      
      
      
       -> Partition
       -> Format
       -> Mount
       







Then we will dive into the menu option of the disk:



       command: #fdisk /dev/sdd
    
    
    
    




After diving into the menu we will part the disk:
            
            
            -> 'n' to create new Partition
            -> select partition number
            -> select starting sector number
            -> Ending sector OR size of the partition in {+ K,G,M} (+5G)
            -> 'q' to quit the menu option








The parted disk needs to be allocated driver and formated:



       command: #udevadm settle (allocates the driver)
             #mkfs.ext4 /dev/sdd1 (formats the partiotn and adds a FS of the type EXT4)
             
             
             






The parted and formatted partition needs to be mounted to a directory to in use or to add an entrypoint:





       command: #mount /dev/sdd1 /dn   (mounting the partiotn to a directory)
        
        
        
        






As the DataNode directory is ready we will restart the DN service:



       command: #hadoop-daemon.sh start datanode









Now we will check our storage allocated by DataNode to NameNode again:



              -> WebUI(IP:50070)
    The size allocated is similar to the partition we created. 




    
 
 
