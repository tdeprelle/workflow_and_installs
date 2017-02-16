# Benchmarking your HDD or SSD and your NVIDIA-GPU

#### Disk

We are going to benchmark the speed of reading of your disk.
First find where is mounted your disk with the "Disks" GUI application. It should be something like */dev/YOUR_DISK* .
You can now start the benchmark.

``` sh
$ sudo hdparm -Tt /dev/YOUR_DISK
```

On my serveur SSD :
Timing cached reads:   23312 MB in  1.99 seconds = 11703.38 MB/sec
Timing buffered disk reads: 1540 MB in  3.00 seconds = 513.28 MB/sec

On my laptop SSD :
Timing cached reads:   21448 MB in  2.00 seconds = 10737.70 MB/sec
Timing buffered disk reads: 3820 MB in  3.00 seconds = 1273.17 MB/sec

On my laptop HDD :
Timing cached reads:   20816 MB in  2.00 seconds = 10420.64 MB/sec
Timing buffered disk reads: 408 MB in  3.01 seconds = 135.65 MB/sec


#### GPU NVIDIA
I assume that you have a Nvidia GPU with Cuda installed. If not [install_cuda](https://github.com/ThibaultGROUEIX/workflow_and_installs/tree/master/torch_workflow.md).

Cuda comes with a set of samples that allow you to test your GPU. You need to compile them first.
``` sh
$ cd /usr/local/cuda/samples/
$ make
```
Or if you have n proccessors :
``` sh
$ make -jn
```

Then find the executable and launch a Benchmark :
``` sh
$ cd ./bin/x86_64/linux/release/
$ ./nbody -benchmark -numbodies=256000
```

Here are the results for different GPU I encountered in my life. Feel free to send me your result, I will add them and make a clean table if need be.

* *TITAN X (Pascal)*
256000 bodies, total time for 10 iterations: 1727.083 ms
= 379.461 billion interactions per second
= 7589.210 single-precision GFLOP/s at 20 flops per interaction
./deviceQuery

* *GeForce GTX TITAN X*
256000 bodies, total time for 10 iterations: 3688.793 ms
= 177.662 billion interactions per second
= 3553.249 single-precision GFLOP/s at 20 flops per interaction

* *GTX970M*
256000 bodies, total time for 10 iterations: 9148.667 ms
= 71.634 billion interactions per second
= 1432.690 single-precision GFLOP/s at 20 flops per interaction