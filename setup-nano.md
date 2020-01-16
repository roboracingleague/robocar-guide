1. Jetson nano initial setup

https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#intro

We recommend to disable automatic updates checks

In Settings/Network, for wired connection, IPV4 settings, set method "Shared with other computers"

Check your Nano is in power max mode (should be default now)
``` sudo nvpmodel -q ```

2. Install required components

``` 
sudo apt update
sudo apt install python3-pip libzmq3-dev build-essential libatlas-base-dev gfortran python3-scipy
``` 

``` 
# install nodejs 10.16+
VERSION=v10.17.0
DISTRO=linux-arm64
wget https://nodejs.org/dist/$VERSION/node-$VERSION-$DISTRO.tar.gz
sudo mkdir -p /usr/local/lib/nodejs
sudo tar -xvf node-$VERSION-$DISTRO.tar.gz -C /usr/local/lib/nodejs 
# Link binaries to /usr/bin
sudo ln -s /usr/local/lib/nodejs/node-$VERSION-$DISTRO/bin/node /usr/bin/node
sudo ln -s /usr/local/lib/nodejs/node-$VERSION-$DISTRO/bin/npm /usr/bin/npm
sudo ln -s /usr/local/lib/nodejs/node-$VERSION-$DISTRO/bin/npx /usr/bin/npx

# install tensorflow
# Reference https://docs.nvidia.com/deeplearning/frameworks/install-tf-jetson-platform/index.html
sudo apt install libhdf5-serial-dev hdf5-tools libhdf5-dev zlib1g-dev zip libjpeg8-dev
sudo pip3 install -U pip testresources setuptools
sudo pip3 install -U numpy==1.16.1 future==0.17.1 mock==3.0.5 h5py==2.9.0 keras_preprocessing==1.0.5 keras_applications==1.0.8 gast==0.2.2 enum34 futures protobuf

sudo pip3 install --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v43 tensorflow-gpu

# remove incompatible library
sudo pip uninstall -y enum34
```

3. Install donkey python module

```
git clone https://github.com/roboracingleague/robocar-donkey.git donkey
sudo pip3 install -e donkey
```

4. Create a "car instance" from template

```
mkdir d2
cp donkey/donkeycar/config-defaults.py d2/config.py
cp donkey/donkeycar/donkey2-jetson.py d2/manage.py
```