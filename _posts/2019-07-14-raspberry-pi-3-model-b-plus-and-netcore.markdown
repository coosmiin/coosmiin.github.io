---
layout: single
title:  "Raspberry Pi 3 Model B+ and .Net Core"
date:   2019-07-14 +0200
categories: raspberrypi netcore
clasees: wide
---

**Goal:** Run a hello world .Net Core application on a Raspberry Pi. At the time of this writing the Pi used is Pi 3 Model B+ and .Net Core version 2.1. The idea was to just run the application on the Pi while it is previously created and publish on another environment. Therefore the Pi needs to know only about the .Net Core runner and not the whole SDK.

For a starter I tried to use [.NET Core on Raspberry Pi](https://github.com/dotnet/core/blob/master/samples/RaspberryPiInstructions.md) instructions. If creating a dummy app with .Net Core and publishing it worked smoothly making the Pi ready takes some steps:
1. Install [Raspbian](https://www.raspberrypi.org/downloads/raspbian/) on your Pi
-- Download the Linux image (I chose Raspbian Stretch with desktop)
-- [Burn it to a micro SD card with Etcher](https://www.raspberrypi.org/documentation/installation/installing-images/)
2. [Enable SSH on your Pi](https://www.raspberrypi.org/documentation/remote-access/ssh/README.md). It can be done even without connecting your Pi to a monitor. However you will need to find out your IP address on the Pi to be able to connect through SSH. I did that while on the Pi by using `sudo ifconfig`. Now you can `ssh pi@[your pi's ip]`
3. Copy your app to PI with [Secure Copy](https://en.wikipedia.org/wiki/Secure_copy) using command line on the source computer
```
scp -r foldername pi@[your pi's ip]
```
`pi` is the root user and the files are copied on its root folder. `scp` command can be enhanced to copy the files anywhere on the Pi.

4. Install .Net Core runtime on the Pi (thanks [Hanselman](https://www.hanselman.com/blog/BuildingRunningAndTestingNETCoreAndASPNETCore21InDockerOnARaspberryPiARM32.aspx)). 
```
sudo apt-get -y update  
sudo apt-get -y install libunwind8 gettext  
wget https://dotnetcli.blob.core.windows.net/dotnet/aspnetcore/Runtime/2.1.4/aspnetcore-runtime-2.1.4-linux-arm.tar.gz  
sudo mkdir /opt/dotnet  
sudo tar -xvf aspnetcore-runtime-2.1.4-linux-arm.tar.gz -C /opt/dotnet/  
sudo ln -s /opt/dotnet/dotnet /usr/local/bin  
dotnet --info
```
Note that the actual url for the .Net Core Runtime was copied from the [docker file](https://github.com/dotnet/dotnet-docker/blob/master/2.1/runtime/stretch-slim/arm32v7/Dockerfile) as suggested by Scott.

5. Run your `helloworld` app
```
ssh pi@172.27.0.1
/* command to move to your's app folder*/
chmod 755 ./helloworld
./helloworld
```
By [`chmod 755`](https://askubuntu.com/questions/932713/what-is-the-difference-between-chmod-x-and-chmod-755) you just give the necessary permissions for that file.