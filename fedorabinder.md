Here are the steps to install ashmem and binder kernel modules for using WayDroid on Fedora Linux:

1. Install the dependencies:

```
sudo dnf install autoconf automake gcc gcc-c++ libstdc++-devel libstdc++-static make mesa-libGL-devel zlib-devel
```

2. Clone the ashmem and binder repositories:

```
git clone https://android.googlesource.com/platform/system/core/+/master/ashmem
git clone https://android.googlesource.com/platform/system/extras/+/master/simpleperf/doc/binder.git
```

3. Build and install ashmem:

```
cd ashmem
./autogen.sh
./configure
make
sudo make install
```

4. Build and install binder: 

```
cd binder
make 
sudo make install
```

5. Load the kernel modules:

```
sudo modprobe ashmem_linux
sudo modprobe binder_linux
```

6. Add them to load on boot:

```
echo "ashmem_linux" | sudo tee -a /etc/modules-load.d/android.conf
echo "binder_linux" | sudo tee -a /etc/modules-load.d/android.conf
```

That should install the required kernel modules for WayDroid. Remember to load the modules or reboot after each kernel update. Let me know if you have any other questions!
