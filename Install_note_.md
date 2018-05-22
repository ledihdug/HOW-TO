# How To
## 1. Install Anacoda

  https://www.digitalocean.com/community/tutorials/how-to-install-the-anaconda-python-distribution-on-ubuntu-16-04
  
  In case of mistake:
    ```
    $ export PATH=$PATH:$HOME/anaconda3/bin
    ```
 
## 2.Install Driver and Cuda
 
 https://qiita.com/sasayabaku/items/2323a2c501e58c0621b6
 
 ## 3. Install Cudnn trước khi install Tensorflow
 
 http://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html
 
  - Cudnn đã được download về /home/dung
 
  ## 4. Create a new Conda environment 
  ```
  $conda create -n myenv python=3.6
  ```
 
##  5.Install Tensorflow to myenv
 # Hien tai dang dung CUDA 8.0 (2018.5.23)
  - Activate myenv 
  ```
  $source activate myenv
  ```
  - Install tensorflow as following
 
 https://www.tensorflow.org/install/install_linux#InstallingAnaconda
 
 Latest tensorflow-gpu doen't work with cuda9.1 ---> using cuda 8.0 
  https://qiita.com/mitsuharu_e/items/ecff16bdbcb795a86433
 
 ---> New way to install tf to CUDA 9.1
 http://www.python36.com/install-tensorflow141-gpu/
  
  http://www.codesofinterest.com/2016/11/setting-up-keras-anaconda-ubuntu.html
 
 Lưu ý theano requirements ---> kenas backend
 
 https://keras.io/ja/backend/
 
 http://deeplearning.net/software/theano/install_ubuntu.html
 
 ## Jupyter Notebook
 
 https://qiita.com/cafedrip/items/f944f72016ced4ff4361

https://devtalk.nvidia.com/default/topic/1024342/cuda-setup-and-installation/unable-to-uninstall-cuda-9-0-completely-and-install-8-0-instead/


# location issue ---> I guess beacause we used EN in JAP
https://askubuntu.com/questions/162391/how-do-i-fix-my-locale-issue

# Jupyter cannot iport tensorflow ---- > 

Reinstall Jupyter in env
```
conda install jupyter
```
