---
layout: post
title:  "Getting started in pentesting (with DVWA)"
date:   2015-09-12 15:00:37
categories: hacking web applications pentesting 
---


Damn Vulnerable Web Application (DVWA) is a great tool to get started with web application pentesting.
It lets you experiment with the basics and it doesn't require you to install additional tools.
In this post, we'll explain how to install and configure it.

The easiest way to get started is to just download the "live cd". You can find it [here]( http://www.dvwa.co.uk/DVWA-1.0.7.iso)
You'll also need to download VMware Player to run the live cd. Go ahead and download that [here](https://my.vmware.com/web/vmware/free#desktop_end_user_computing/vmware_player/6_0)

First install VMware player, just follow the steps in the installer (next, next,..., finish).
When the player is installed (you might have to reboot), start the application. You should see a screen resembling this:

![Create new machine](/assets/ScreenClip1.png)

Click on "Create a New Virtual Machine" and select "Installer disk image file". Use the "Browse" button to select the DVWA iso you downloaded earlier.

![Create new machine](/assets/ScreenClip2.png)

On the next screen, VMware will ask you which guest operating system to use. Just select "Linux" and use version "Debian 7 64bit"

![Create new machine](/assets/ScreenClip3.png)

Click next and give your virtual machine a name you like. I'm using "DVWA".


![Create new machine](/assets/ScreenClip4.png)

Click next. On the following screen, the defaults are ok and you can just click next again. Finally click finish to complete the virtual machine creation.
Now you should see a screen with the new virtual machine in the "powered off" state.
Click on "Play virtual machine". Now just wait a bit until the machine is booted. It can take a while, but you should finally see the following screen.

![Create new machine](/assets/ScreenClip5.png)

Now DVWA is booted, but you still need to know where to find it. Click inside the screen and type the following: "ifconfig eth0" (that's a zero).
Write down the text in the circle, that's the ip where you'll find DVWA.

![Create new machine](/assets/ScreenClip7.png)


Hit "ctrl+alt" to escape the VM and start a browser (I use chrome, but it doesn't matter which one)
Type the ip address you wrote down in the address bar and hit enter. You should be greeted by a login screen.
You can log in by typing "admin" as the username and "password" as password.

![Create new machine](/assets/ScreenClip6.png)

Now you're almost done. Find the button in the lower left corner that's marked "DVWA Security".
Click it and select security "low" on the resulting page. Hit "submit" to confirm.

Now you're ready to get started. I suggest you begin with "XSS Reflected". Make sure to read the articles in "More info"!

I'll post some tutorials on how to take on the challenges in the near future.
Stay tuned and good luck!


