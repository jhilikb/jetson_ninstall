# jetson_ninstall
Install cuda related stuff in jetson nano

1.You have to insert your sdcard and check partition name..use the following  
  
sudo fdisk -l  
lsblk -f  

2. Create partition on your sdcard
sudo mkfs -t ext4 /dev/mmcblk1p1

3. Mount your sdcard and cd in it
sudo mount /dev/mmcblk1p1 /sdcard
  
cd /sdcard/   
sudo mkdir fol  

4.Move your docker folder on your sdcard and link it  
sudo mv /var/lib/docker /sdcard/fol/  
sudo ln -s /sdcard/fol/docker /var/lib/docker  
sudo ln -s /sdcard/fol/docker /var/lib/docker



