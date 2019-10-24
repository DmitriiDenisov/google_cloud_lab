# google_cloud_lab
Video instructions: https://www.youtube.com/watch?v=W-FqRBoyTgw&t=897s

Text instructions: http://amunategui.github.io/fast-gpu-gcloud/

You can follow the instructions in sequence, but after all, you will need to make a few changes, namely:

### Quotas:

There is an incorrect quota request in video instructions. To correctly request a quota, type "quotas" and select the following filters:

![alt-text-1](https://i.ibb.co/C8F82Mh/1.png "title-1")

## Compability:

When installing according to his (and another's) instructions, the versions of CUDA, Cudnn and tensorflow-gpu that do not support each other are installed. Look carefully at the versions of CUDA, Cudnn, and tensorflow-gpu installed. The problem is that they are not all compatible with each other. And if you install incompatible versions, then when importing tensorflow (already inside python), the libcublas.so.10.0 error will occur: cannot open shared object

In order to avoid it follow this table: https://www.tensorflow.org/install/source#tested_build_configurations

At the same time, I tried the combination from the table: CUDA 8, CUdNN 6, tensorflow_gpu-1.4.0 and still did not work
The final configuration in which it worked for me: CUDA 9, cuDNN v7.1.4 Runtime Library for Ubuntu16.04 (Deb), tensorflow_gpu-1.12.0

Link to that version of cuDNN:

https://developer.nvidia.com/compute/machine-learning/cudnn/secure/v7.1.4/prod/9.0_20180516/Ubuntu16_04-x64/libcudnn7_7.1.4.18-1_cuda9.0_amd64


### Summary: 
1) Follow and do all the instructions from the website, while installing CUDA 9, cuDNN v7.1.4 Runtime Library for Ubuntu16.04 (Deb)
2) sudo pip3 uninstall tensorflow-gpu
3) sudo pip3 install tensorflow-gpu==1.12.0


### To run locally in terminal: 
RSA keys and so forth
https://www.youtube.com/watch?v=R8C66NwMJLs

### Run in Pycharm:
Professional version is required. In the window selection of the interpreter: select ssh, leave port 22, then follow the instructions.

![alt-text-1](https://i.ibb.co/jyZFc6c/2.png "title-1")


### To check the GPU:
Run test_gpu.py file from this repository

### ssh login with password (without public/secret key pair):
1. ```sudo vim /etc/ssh/sshd_config```. Change following row: 

"PasswordAuthentication yes"

2. ```sudo service ssh restart```
3. ```sudo su```
4. ```passwd \<username\>``` (for example passwd dmitryhse). This will reset user’s password
5. exit (exit from sudo mode)
6. ```ssh \<login\>@\<ip\>``` (for example ssh dmitryhse@35.188.90.126)

### Mount remote server file system as disk on your Mac:

https://www.youtube.com/watch?v=ubfeyVtyFJc

Example of running command:

 ```sshfs dmitryhse@35.208.27.233:/home /Users/Dmitry/Desktop/folder -ovolname=remonte_front_VM```
 
 ```umount -f /Users/Dmitry/Desktop/folder```
 
 Specifies key:
 ```sshfs dmitryhse@35.208.27.233:/home /Users/Dmitry/Desktop/folder -ovolname=remonte_front_VM -o IdentityFile=/path/to/key```

### Open port
https://www.youtube.com/watch?v=JmjqPpQdtW8

### Launch Jupyter Notebook in Google Cloud:
1. Open port
2. ``` jupyter-notebook --no-browser --port=<PORT-NUMBER> ```

### Create Windows remote Desktop:
https://www.youtube.com/watch?v=p5wl1s5gKY0&t=270s

Connect to remote Windows machine use this app:
https://apps.apple.com/ru/app/microsoft-remote-desktop-10/id1295203466?mt=12

### Error: "Accelerators are not available for instances with a shared physical core"
You can encounter with this error when trying to enable GPU when you have Machine Type: Shared core.
I.e it might be f1-micro or g1-small.
1) Stop VM
2) Change 'Machine type' from 'Shared core' to 'Standard'
3) Click 'Save'
4) Click 'Edit' and then add GPU
5) Check that GPU is available: `sudo lshw -C display`
