# ev3dev
From the ev3dev website: ev3dev is a Debian Linux-based operating system that runs on several LEGO® MINDSTORMS compatible platforms including the LEGO® MINDSTORMS EV3 and Raspberry Pi-powered BrickPi.

The main reason for using ev3dev is to allow us to run python on it. However as it is a linux kernel, it has far more uses that the basic OS EV3 provides.

This tutorial helps set up ev3dev on an EV3, SSH and set up git on it. Git is a useful version control tool that in this case, allows us to upload code to the EV3. This allows us to code on and IDE or text editor on our local machine, then upload it to the EV3.

This was done on my Ubuntu 20.04 machine

## Flashing the sd card
To set up ev3dev, get a microsd card and download the image file [here](https://www.ev3dev.org/downloads/)

Download [etcher](https://www.etcher.net/) to flash the .img file onto the sd card
Now just put the sd card into the ev3 and boot it up, it should take a few minutes for the first time

## SSH
I followed this [tutorial](https://www.ev3dev.org/docs/tutorials/connecting-to-the-internet-via-usb/) which allowed me to SSH into ev3dev

This is important for setting up git
If you are on windows, use [putty](https://www.putty.org/) to ssh

## Git
Follow these commands, if there is an error, you could reference this [page](https://www.ev3dev.org/docs/tutorials/setting-up-python-pycharm/) to try and debug

```bash
ssh robot@ev3dev.local

#default password is maker

$ sudo apt-get update
$ sudo apt-get install git
$ mkdir project
$ cd project
$ mkdir project.git
$ git init --bare project.git
$ vim project.git/hooks/post-receive

#this will open the file, press i to go to insert mode and add the following two lines

#!/bin/sh
git --work-tree=/home/robot/project --git-dir=/home/robot/project/project.git checkout -f

then press esc and type :x and enter to exit vim

$ chmod +x project.git/hooks/post-receive
$ git config --global user.email "you@example.com"
$ git config --global user.name "Your Name"
$ git add .
$ git commit -m "First Commit"
$ git remote add origin robot@ev3dev:/home/robot/project/project.git
$ git push --set-upstream origin master
```
