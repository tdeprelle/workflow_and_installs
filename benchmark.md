# Benchmarking your HDD or SSD and your NVIDIA-GPU

#### Disk

We are going to benchmark the speed of reading of your disk.
First find where is mounted your disk with the "Disks" GUI application. It should be something like */dev/YOUR_DISK* .
You can now start the benchmark.

``` sh
$ sudo hdparm -Tt /dev/YOUR_DISK
```


Disk | Timing cached reads | Timing buffered disk reads
--- | --- | ---
*serveur SSD* | 11703.38 MB/sec | 513.28 MB/sec 
*On my laptop SSD* | 10737.70 MB/sec | 1273.17 MB/sec 
*On my laptop HDD* | 10420.64 MB/sec | 135.65 MB/sec



#### GPU NVIDIA
I assume that you have a Nvidia GPU with Cuda installed. If not [install cuda 8](https://github.com/ThibaultGROUEIX/workflow_and_installs/tree/master/torch_workflow.md).

Cuda comes with a set of samples that allow you to test your GPU. You need to compile them first.
``` sh
$ cd /usr/local/cuda/samples/
$ make
```
Or if you have n processors :
``` sh
$ make -jn
```

Then find the executable and launch a Benchmark :
``` sh
$ cd ./bin/x86_64/linux/release/
$ ./nbody -benchmark -numbodies=256000
```

Here are the results for different GPU I encountered in my life. Feel free to send me your result, I will add them.

GPU | cuda | total time for 10 iterations (ms) | billion interactions per second | single-precision GFLOP/s at 20 flops per interaction
--- | --- | --- | --- | ---
*TITAN X (Pascal)* | 8 | 1727 | 379 | 7589
*GeForce GTX TITAN X* | 8 | 3688 | 177 | 3553
*GTX970M* | 8 | 9148 | 71 | 1432


[![Analytics](https://ga-beacon.appspot.com/UA-91308638-2/github.com/ThibaultGROUEIX/workflow_and_installs/benchmark.md?pixel)](https://github.com/ThibaultGROUEIX/workflow_and_installs/)
