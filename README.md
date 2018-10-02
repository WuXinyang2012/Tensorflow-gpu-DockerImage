# Tensorflow docker image    

## Aufgabe:  
	1, Ein Dockerimage erstellen;  
	2, Die nötige Software einbinden (Folie 2+3);  
	3, Das Tensorflow-Skript „Hello World“ via Docker ausführen (Folie 4);  
	4, Das Vorgehen detailliert dokumentieren um daraus ein Tutorial erstellen zu können.  

#### Installation Platform: Ubuntu 18.04 LTS, Nvidia driver-390.48, docker 18.06.1-ce.  

### 1, Install nvidia-docker  
The nvidia-docker is a container runtime for docker, offering cuda and cudnn runtime support.  
[Installation](https://github.com/NVIDIA/nvidia-docker/blob/master/README.md)  


### 2, Configure Tensorflow-gpu image.  
Download tensorflow-gpu image and start a container.  
[Instruction](https://www.tensorflow.org/install/docker)  

#### 2.1 Download tensorflow-gpu image  
```Bash
docker pull tensorflow/tensorflow:latest-gpu
```

#### 2.2 Start a container with nvidia runtime support  
```Bash
//The container is named as "bash" in this example
docker run --runtime=nvidia -it --name=bash tensorflow/tensorflow:latest-gpu bash
```

### 3, Install Anaconda in container  
#### 3.1 Start container and attach it to console.  
```Bash
docker start bash
docker attach bash
```

#### 3.2 Install Anaconda  
```Bash
apt install wget
cd /home
wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/Anaconda2-5.2.0-Linux-x86_64.sh
bash Anaconda2-5.2.0-Linux-x86_64.sh
```

After installation, create conda environment.  
```Bash
conda create -n tensorflow python=2.7
```

Then, install tensorflow-gpu support inside this env.  
```Bash
source activate tensorflow
conda install -c conda-forge tensorflow-gpu
```


--------------------------------


Now, this tensorflow-gpu docker image is well prepared. You can start the "bash" container and test the following simple script in Python2 environment:  

```Python
import tensorflow as tf
import numpy as np
import PIL
import scipy

hello = tf.constant('Hello, TensorFlow!')
sess = tf.Session()

print(sess.run(hello))
```
