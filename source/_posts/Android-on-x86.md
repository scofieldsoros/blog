title: Android on x86
date: 2015-09-10 06:59:09
tags:
---

### Install android x86 in vmware fusion

acturally, the process is pretty simple, and there are dozens of articles introducing that.

the probleam I have met when install Android on vmware is the Network adapter. I didn't see the *eth0* interface when installed.

after a little search, I found the solution. Pretty simple too.

1. create the Android system first, don't start it immediately
2. edit the *XXX.vmx* file in the VM's directory.
3. change the line *ethernet0.virtualDev = "e1000"* to *ethernet0.virtualDev = "vlance"* and save the file
4. start the VM. There should be a network adaptor called *eth0* now. If the network type is set to NAT, the VM should have internet connection already, if now, just do some configuration.
