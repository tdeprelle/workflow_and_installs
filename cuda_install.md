# install nvidia-driver for ubuntu 16.04

```
sudo apt-get purge nvidia*
sudo apt-get install nvidia-384
sudo apt-get install g++ freeglut3-dev build-essential libx11-dev \
    libxmu-dev libxi-dev libglu1-mesa libglu1-mesa-dev
sudo reboot
```
# testing

```
nvidia-smi
nvidia-detector
```

### If error before grub : 
-add "nomodeset" after quiet splash in boot options

open a terminal ctrl alt f1, and

```sudo apt-get purge nvidia*```

"download relevant file from nvidia and then

```
gcc --version
uname -r
```


##### possible errors 
/usr/bin/ld: cannot find -lcuda

This is solved by making a symbolic link for libcuda.so out of /usr/lib/NVIDIA-319/ and into /usr/lib/
```
sudo ln -s /usr/lib/NVIDIA-319/libcuda.so /usr/lib/libcuda.so
```
for cuda 7.5 test that you have gcc > 4.8.2 and kernel > 3.16



```sudo apt-get install openmpi-bin openmpi-common libopenmpi-dev ```#package mpicc needed to make OpenMPI.cu, source http://www.somewhereville.com/?p=1896

If you’re working through the build process and hit the error, run a “make clean” before rerunning.

Check out the results of 
```
./deviceQuery
deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 9.0, CUDA Runtime Version = 9.0, NumDevs = 4
```

* CUDA Driver Version is the maximum version of CUDA your NVIDIA driver supports. In this case, if I want to update to cuda 9.1 available now, I have to update my NVIDIA-driver which is always risky so I stick to 9.0 for now.
*  CUDA Runtime Version is the actual version of CUDA installed.

# Good reference to install 7.5 and 8. 

important : use .run file from NVIDIA and don't accept install of new driver !

https://www.pugetsystems.com/labs/hpc/Install-Ubuntu-16-04-or-14-04-and-CUDA-8-and-7-5-for-NVIDIA-Pascal-GPU-825/

and https://www.pugetsystems.com/labs/hpc/NVIDIA-CUDA-with-Ubuntu-16-04-beta-on-a-laptop-if-you-just-cannot-wait-775/

get cuda 8, 7.5, 9 from nvidia website. Remember to take the .run :

####list options
```./cuda_7.5.18_linux.run --help```
####use sudo if neccessary
```
chmod 755 cuda_*
./cuda_7.5.18_linux.run --silent --toolkit --samples --samplespath=/usr/local/cuda-7.5/samples --override
./cuda_8.0.27_linux.run --silent --toolkit --samples --samplespath=/usr/local/cuda-8.0/samples --override
./cuda_9.0.176_384.81_linux.run --silent --toolkit --samples --samplespath=/usr/local/cuda-9.0/samples --override
```
#####to switch cuda versions
```
sudo rm /usr/local/cuda
sudo ln -s /usr/local/cuda-7.5 /usr/local/cuda
```
#####especially for 7.5
```
sed -i '/unsupported GNU version/ s/^/\/\//' /usr/local/cuda-7.5/include/host_config.h
sed -i '/unsupported GNU version/ s/^/\/\//' /usr/local/cuda-8.0/include/host_config.h
```
#####not sure it is needed
```
find /usr/local/cuda-7.5/samples -type f -exec sed -i 's/nvidia-3../nvidia-367/g' {} +
find /usr/local/cuda-8.0/samples -type f -exec sed -i 's/nvidia-3../nvidia-367/g' {} +
```
#####add these three to .bashrc
```
export PATH=$PATH:/usr/local/cuda/bin
export CUDADIR=/usr/local/cuda
export GLPATH=/usr/lib
```
#compile samples
```
cd /usr/local/cuda-7.5/samples
sudo make
/usr/local/cuda-8.0/samples
sudo make

sudo reboot
```
#testing

```./nbody -benchmark -numbodies=256000```
TITAN X (Pascal) 
256000 bodies, total time for 10 iterations: 1727.083 ms
= 379.461 billion interactions per second
= 7589.210 single-precision GFLOP/s at 20 flops per interaction
./deviceQuery

GeForce GTX TITAN X (already in use)
256000 bodies, total time for 10 iterations: 3688.793 ms
= 177.662 billion interactions per second
= 3553.249 single-precision GFLOP/s at 20 flops per interaction

GTX970
256000 bodies, total time for 10 iterations: 9148.667 ms
= 71.634 billion interactions per second
= 1432.690 single-precision GFLOP/s at 20 flops per interaction


[![Analytics](https://ga-beacon.appspot.com/UA-91308638-2/github.com/ThibaultGROUEIX/workflow_and_installs/initial_steps.md?pixel)](https://github.com/ThibaultGROUEIX/workflow_and_installs/)
