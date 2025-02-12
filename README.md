# jetson_ninstall
Install cuda related stuff in jetson nano

# 1.You have to insert your sdcard and check partition name..use the following  
  
sudo fdisk -l  
lsblk -f  
  
# 2. Create partition on your sdcard
sudo mkfs -t ext4 /dev/mmcblk1p1

# 3. Mount your sdcard and cd in it  
sudo mount /dev/mmcblk1p1 /sdcard
  
cd /sdcard/   
sudo mkdir fol  

# 4.Move your docker folder on your sdcard and link  
sudo mv /var/lib/docker /sdcard/fol/  
sudo ln -s /sdcard/fol/docker /var/lib/docker  
  
# 5. Install cudnn  
sudo apt-get install libcudnn8 libcudnn8-dev  -y  

# 6. Define folder path same as where you cloned the git and cd into it  

fol='  path where you have cloned '  
cd $fol  
  
# 7. Set your nvidia runtime  

sudo cp  gpu_ready/nvidia_runtime/libnvidia-container.so.0.10.0    /usr/lib/aarch64-linux-gnu/  
sudo cp gpu_ready/nvidia_runtime/libnvsample_cudaprocess.so      /usr/lib/aarch64-linux-gnu/  
sudo cp gpu_ready/nvidia_runtime/nvidia-container-*  /usr/bin/  
sudo cp gpu_ready/nvidia_runtime/daemon.json      /etc/docker/daemon.json  
sudo cp gpu_ready/csvs/*               /etc/nvidia-container-runtime/host-files-for-container.d/  

# 8. Download contents into your gpu_ready/tensorrtfiles folder following directions given in gpu_ready/tensorrtfiles/download file
  
# 9. Now set the tensorrt files  

sudo cp  gpu_ready/tensorrtfiles/incaarch64/*  /usr/include/aarch64-linux-gnu/  
sudo cp  gpu_ready/tensorrtfiles/libaarch64/*  /usr/lib/aarch64-linux-gnu/ 

cd /usr/lib/aarch64-linux-gnu/  
sudo ln -sf libnvinfer_plugin.so.8.0.1 libnvinfer_plugin.so   
sudo ln -sf libnvinfer_plugin.so.8.0.1 libnvinfer_plugin.so.8  
sudo ln -sf libnvinfer.so.8.0.1 libnvinfer.so  
sudo ln -sf libnvinfer.so.8.0.1 libnvinfer.so.8  
sudo ln -sf libnvonnxparser.so.8.0.1 libnvonnxparser.so  
sudo ln -sf libnvonnxparser.so.8.0.1 libnvonnxparser.so.8  
sudo ln -sf libnvparsers.so.8.0.1 libnvparsers.so  
sudo ln -sf libnvparsers.so.8.0.1 libnvparsers.so.8  
  
cd $fol  
  
sudo cp  -r gpu_ready/tensorrtfiles/pyddist/*   /usr/lib/python3.6/dist-packages/  
sudo cp  -r  gpu_ready/tensorrtfiles/tensorrt   /usr/src/  




