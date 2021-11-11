

### Realsensor

Download  https://github.com/IntelRealSense/librealsense/releases/ 
```
cd ~
wget https://github.com/IntelRealSense/librealsense/archive/refs/tags/v2.49.0.zip
unzip v2.49.0.zip
cd ~/librealsense-2.49.0
CUDACXX=/usr/local/cuda-10.2/bin/nvcc
mkdir build
cd build
export PATH=$PATH:/usr/local/cuda-10.2/bin/
cmake ../ -DFORCE_RSUSB_BACKEND=ON -DBUILD_PYTHON_BINDINGS:bool=true -DPYTHON_EXECUTABLE=/usr/bin/python3.6 -DCMAKE_BUILD_TYPE=release -DBUILD_EXAMPLES=true -DBUILD_GRAPHICAL_EXAMPLES=true -DBUILD_WITH_CUDA:bool=true
make -j4
sudo make install

echo "export PATH=$PATH:~/.local/bin
> export PYTHONPATH=$PYTHONPATH:/usr/local/lib
> export PYTHONPATH=$PYTHONPATH:/usr/local/lib/python3.6/pyrealsense2" >> ~/.bashrc

cd ~/librealsense-2.49.0
sudo cp config/99-realsense-libusb.rules /etc/udev/rules.d/
sudo udevadm control --reload-rules
sudo udevadm trigger
realsense-viewer
```

update your PYTHONPATH environment variable to add the path to the pyrealsense library
```
export PYTHONPATH=$PYTHONPATH:/usr/local/lib
```
Alternatively, copy the build output (```librealsense2.so``` and ```pyrealsense2.so```) next to your script.
Note: Python 3 module filenames may contain additional information, e.g. ```pyrealsense2.cpython-35m-arm-linux-gnueabihf.so```)

### For librealsense-2.49.0
.so files are inside /librealsense-2.49.0/build/wrappers/python.
Please copy them(```pyrealsense2.cpython-36m-aarch64-linux-gnu.so.2.49.0```, ```pyrealsense2.cpython-36m-aarch64-linux-gnu.so.2.49```, ```pyrealsense2.cpython-36m-aarch64-linux-gnu.so.```) next to your script or it will pop up module issue.
