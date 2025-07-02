# 🏡HOME LAB ENVIRONMENT

**✅PROJECT OVERVIEW**

In this project, I intend to set up a virtualised home lab environment on my MacBook using UTM. A UTM is an open-source virtualisation software that allows mac users to use multiple operating systems in virtual machines using QEMU. This UTM will allow me to run Windows Operating System on my MacBook. I am building this home lab to gain hands on experience in Windows system administration, networking, PowerShell scripting, and learn security practices which will be beneficial in an enterprise environment.

**💻TOOLS USED**

1. **UTM App**: This helped me create, configure and manage my virtual machine
2. **QEMU:** It is a powerful source hardware emulator that ensures the virtualisation of ARM, x64 and other architectures. I didn’t interact with this directly, the UTM handled everything for me.
3. **Windows 11 ARM64 ISO:** This is a special version of Windows; I used it to install Windows on my virtual machine.
4. **SPICE Guest Tools & QEMU Drivers:** These are essential to ensure optimal performance of the Virtual machines.
5. **VirtIO Drivers:** Important for network connectivity.

**🛠️SETUP INSTRUCTIONS**

1. **INSTALLING THE UTM**
- I visited  [https://mac.getutm.app](https://mac.getutm.app/) to download the UTM
- After the download, i dragged the .dmg file into my application folder.

1. **DOWNLOADING THE WINDOWS 11 ARM64 ISO**

There are two main methods of downloading the Windows 11 ARM64 ISO  

- You either download it from the Crystal Fetch app

![Image 24-06-2025 at 13.56.jpeg](%F0%9F%8F%A1HOME%20LAB%20ENVIRONMENT%2021c2b90cbf228071a871df3a83c9635e/Image_24-06-2025_at_13.56.jpeg)

- Or you visit [https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewARM64](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewARM64) to download .

I prefered to download it from the Crystal Fetch App beacuse it is much faster. Downloading it from the Microsoft app requires you to create an account beforehand, which isnt bad either but the Crystal Fetch App doesnt require this and its pretty much straightforward.

1. **CREATING THE VIRTUAL MACHINE IN UTM**
- I opened the UTM, and clicked on the plus sign to create a new virtual machine

![Image 24-06-2025 at 14.10.jpeg](%F0%9F%8F%A1HOME%20LAB%20ENVIRONMENT%2021c2b90cbf228071a871df3a83c9635e/Image_24-06-2025_at_14.10.jpeg)

- I then selected “Virtualise” which led me to another window from which i chose “Windows”
    
    ![Image 24-06-2025 at 14.12.jpeg](%F0%9F%8F%A1HOME%20LAB%20ENVIRONMENT%2021c2b90cbf228071a871df3a83c9635e/Image_24-06-2025_at_14.12.jpeg)
    

![Image 24-06-2025 at 14.12.jpeg](%F0%9F%8F%A1HOME%20LAB%20ENVIRONMENT%2021c2b90cbf228071a871df3a83c9635e/Image_24-06-2025_at_14.12%201.jpeg)

- I then imported the the Windows ISO file  into the UTM.
- I performed the necessary configurations like setting up the RAM which in my case was 8GB and assigned it 8 CPU cores.
- I also assigned a memory of 64GB and left the other settings as default and saved it.

1. **STARTING THE VM AND INSTALLING WINDOWS**
- I clicked the big play button to start the VM.
- I then followed the Window Setup Wizard Instructions to install the windows.
- After successful installtion, I restarted the Virtual Machine.

![Image 24-06-2025 at 15.27.jpeg](%F0%9F%8F%A1HOME%20LAB%20ENVIRONMENT%2021c2b90cbf228071a871df3a83c9635e/Image_24-06-2025_at_15.27.jpeg)

**👾CHALLENGES AND SOLUTIONS**

1. **BOOT LOOP**

**Problem:**

When I was installing the Windows OS, the VM kept restarting over and over again; what you would call a boot loop. I figured the Windows ISO file was still mounted in the CD/DVD drive which caused VM to boot from it instead of the installed OS.

**Solution:** 

- I completely shutdown the VM
- I then went to the CD/DVD section in VM settings and removed the Windows ISO and ensured that the hard drive was listed first in the boot order.
- I restarted the VM and tried again

The VM then booted from the installed system.

1. **NO NETWORK CONNECTION**

**Problem:**

After setting up the Windows VM, everything worked perfectly fine except the network connection. I wasn’t connected to the internet.

**Diagnosis:**

- I performed a basic network connectivity test by running ping [google.com](http://google.com) in the command prompt. The response i got  was negative indicating no network connection.
- I shut the Windows VM down and went to its settings in the UTM to make sure everything was in tact with the drivers.
- I then reopened the VM and tested for connectivity.
- Upon failure, i had ti manually reinstall the VirtIO drivers for the network card.

**Steps:**

- I visited the [https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/latest-virtio/](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/latest-virtio/) and downloaded the latest version of the VirtIO driver which was the *virtio-win.iso*

![Image 24-06-2025 at 18.56.jpeg](%F0%9F%8F%A1HOME%20LAB%20ENVIRONMENT%2021c2b90cbf228071a871df3a83c9635e/Image_24-06-2025_at_18.56.jpeg)

- After downloading, I mounted the ISO in the UTM

![Image 24-06-2025 at 18.56 (1).jpeg](%F0%9F%8F%A1HOME%20LAB%20ENVIRONMENT%2021c2b90cbf228071a871df3a83c9635e/Image_24-06-2025_at_18.56_(1).jpeg)

- I then booted the VM and installed the driver via device manager.
- Upon successful installation, I then tested the network connectivity again. I recieved a positive response indicating there was connection.

![Image 24-06-2025 at 19.12.jpeg](%F0%9F%8F%A1HOME%20LAB%20ENVIRONMENT%2021c2b90cbf228071a871df3a83c9635e/Image_24-06-2025_at_19.12.jpeg)

![Image 24-06-2025 at 19.13.jpeg](%F0%9F%8F%A1HOME%20LAB%20ENVIRONMENT%2021c2b90cbf228071a871df3a83c9635e/Image_24-06-2025_at_19.13.jpeg)

**🏆LESSON LEARNT**

1. Gained hands-on experience with UTM
2. I’ve learnt how to run Windows on M1 Mac
3. Noticed that boot order have a big effect on installation and startup. 
4. I’ve learnt how to manually install network adapter drivers like the VirtIO
5. Worked on my troubleshooting skills especially when i was resolving the boot order.
6. Most importantly, this project has helped me polish my documentation skills. I’ve realised how important it is to document every step of your work.

**🎯FUTURE GOALS FOR MY HOME LAB**

1. Install Powershell and pratice writing automation scripts.
2. Deploy more VMs like Ubuntu, Linux
3. Make my lab more advanced by:
- practicing networking between VMs
- building a Windows Domain environment
- setting up DHCP, DNS, FTP server
- practicing cybercurity scenarios
- building a virtual network with VLANS and routers