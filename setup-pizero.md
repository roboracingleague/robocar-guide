# Software setup on Raspberry Pi Zero - Companion

1. Get latest Raspbian image and set it up 
- write image on SD Card
- create an empty file named "ssh" on the boot partition

2. Connect to Pi Zero
- default hostname raspberry; user pi; password raspberry
- change default values for user, password and hostname is recommended

3. Install required components
- begin with ``` sudo apt update ```
- nodejs 
```
# nodejs 10.16.+ required 
VERSION=v10.17.0
DISTRO=linux-armv6l
wget https://nodejs.org/dist/latest-v10.x/node-$VERSION-$DISTRO.tar.gz
sudo mkdir -p /usr/local/lib/nodejs
sudo tar -xvf node-$VERSION-$DISTRO.tar.gz -C /usr/local/lib/nodejs 
# Link binaries to /usr/bin
sudo ln -s /usr/local/lib/nodejs/node-$VERSION-$DISTRO/bin/node /usr/bin/node
sudo ln -s /usr/local/lib/nodejs/node-$VERSION-$DISTRO/bin/npm /usr/bin/npm
sudo ln -s /usr/local/lib/nodejs/node-$VERSION-$DISTRO/bin/npx /usr/bin/npx
```

- zmq dev library ``` sudo apt install -y cmake libzmq3-dev ```

4. Install robocar-devices

```
git clone https://github.com/roboracingleague/robocar-devices.git
cd robocar-devices
npm install
```

5. Start your service automatically

This is up to you :-) However, here's a suggested procedure:
- create a start script in home; NODE_ENV allow you to create a personalized configuration yaml. Check out 'npm config.js' 
```
echo "cd /home/pi/robocar-devices && export NODE_ENV=alpha && npm start" > start_service.sh
chmod +x start_service.sh
```
- run the script at startup
```
sudo crontab -e
```
Add a line :

```
@reboot sh /home/pi/start_service.sh >/home/pi/logs/cronlog 2>&1 &
```