# Using Torch, with CUDA, CUDNN, notebooks.


# just not ready yet! Wait a few more days...

sudo apt-get install cmake
sudo apt-get install libreadline-dev
git clone https://github.com/torch/distro.git ~/torch --recursive
cd ~/torch; bash install-deps;
./install.sh
source ~/.bashrc
luarocks install image
luarocks list
sudo apt-get install libmatio2
luarocks install matio #for matlab .mat support
# for uninstall:
# rm -rf ~/torch

# itorch
sudo apt-get install python-pip -y
sudo pip install jupyter
sudo apt-get install python-zmq -y
# Ubuntu
sudo apt-get install libzmq3-dev libssl-dev python-zmq

# Ubuntu 16
luarocks install lzmq
cd lib
git clone https://github.com/facebook/iTorch.git
cd iTorch
luarocks make 

luarocks install display
luarocks install torchnet
luarocks install optnet
# install matlab first
luarocks install mattorch
# debugger for a stand-alone debugger
sudo apt-get install libedit-dev 
luarocks install https://raw.githubusercontent.com/bshillingford/fbdebugger-minimal/master/fbdebugger-standalone-1.rockspec 


###Cudnn from Nvidia (download cudnn from Nvidia webpage : membership connection required)
export PATH=/usr/local/cuda-8.0/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
tar xvzf cudnn-8.0-linux-x64-v5.1.tgz
sudo cp cuda/include/cudnn.h /usr/local/cuda/include
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
#from : https://yangcha.github.io/GTX-1080/

[![Analytics](https://ga-beacon.appspot.com/UA-91308638-2/github.com/ThibaultGROUEIX/KernelMethods_mva/README?pixel)](https://github.com/ThibaultGROUEIX/KernelMethods_mva/)
