# Active-Directory

This is a project where I configure a Windows Domain and Active Directory. The following technology will be used: VirtualBox, Windows Server 2019, and Windows 10 Enterprise. 

**Step 1:** Because I will be using VirtualBox to practice configuring a Windows Domain/Active Directory, I want to make sure that my computer has virtualization capabilities enabled. To do so, I opened up Task Manager and click into the Performance tab. I then clicked into the CPU section, and checked that virtualization is indeed enabled. Refer to the image below.

![Task Man](https://github.com/johnnyh209/Active-Directory/assets/33064730/6ee13245-828c-48a7-8047-1d04eaa564ca)

**Step 2:** With virtualization enabeled, I preceeded to install VirtualBox.

![Install VB](https://github.com/johnnyh209/Active-Directory/assets/33064730/2e508aa2-4ccf-4304-b1de-e02564c47424)

Once the installation has completed, I was presented with the main page of the application:

![VB Front page](https://github.com/johnnyh209/Active-Directory/assets/33064730/fad4d969-f0d5-4b4f-9e11-2285ee01ff93)

**Step 3:** Once VirtualBox was set up, I needed to grab the .iso files for both Windows Server 2019 and Windows 10 Enterprise. Windows Server 2019 will be used as the manager (where we will be configuring Active Directory on), and Windows 10 Enterprise will represent employees (admin (super) users, regular users, guest users).

**Step 4:** With the .iso files on hand, I started off by creating a virtual machine for Windows Server 2019. The first page of the creation wizard deals with naming the virtual machine, choosing a directory to store the virtual machine files on, and choosing an ISO image. 
In the name field, I entered `Windows Server 2019` for the virtual machine’s name so that I can easily identify/differentiate between the numerous virtual machines I will be creating. I then pointed to a directory in which I want the virtual machine to be installed to, and selected the Windows Server 2019 .iso image. I also selected the check box for `Skip Unattended Installation` to speed up the installation process.

![Creating VM part 1](https://github.com/johnnyh209/Active-Directory/assets/33064730/37fb775f-b57d-42d1-bdbe-3e536c2cd412)

The second page of the creation wizard deals with assigning the amount of RAM and virtual CPU count to the virtual machine. In this step, it is important to make sure that you assign enough resources to satisfy the minimum requirements of the operating system that you will be installing. For Windows Server 2019, the requirements are as follows (you can find the requirements in [Microsoft's documentation](https://learn.microsoft.com/en-us/windows-server/get-started/hardware-requirements):

```
Processor:

    1.4 GHz 64-bit processor
    Compatible with x64 instruction set
    Supports NX and DEP
    Supports CMPXCHG16b, LAHF/SAHF, and PrefetchW
    Supports Second Level Address Translation (EPT or NPT)

RAM:

    512 MB (2 GB for Server with Desktop Experience installation option)
    ECC (Error Correcting Code) type or similar technology, for physical host deployments

Storage / Disk Space:

    Minimum: 32 GB

Network Adapters:

    An ethernet adapter capable of at least 1 gigabit per second throughput
    Compliant with the PCI Express architecture specification.
```
For this virtual machine instance, I opted for 4096 MB (~4 GB) of RAM, 2 processor counts, and 50 GB of disk space. Below is an image of my configuration:

![Creating VM part 4](https://github.com/johnnyh209/Active-Directory/assets/33064730/6d133678-0c1e-4302-858c-a85a3f362e8c)

**Step 5:** After the Windows Server 2019 virtual machine was set up, there were a few settings I needed to change. I right-clicked on the virtual machine listed on the front page of the virtual box, and clicked into `Settings`. From there, I headed into `System` and uncheck `Floppy` in the `Boot Order` section. This way, I can ensure that VirtualBox will boot into the .iso image for Windows Server 2019. Next, I head into `Network` in the “Settings” page. By default `NAT` is the network adapter chosen. We will change that to `Bridged Adapter`, pretty much telling VirtualBox to connect the virtual machine to the host system’s (in this case, my computer) network adapter.

![Uncheck Floppy](https://github.com/johnnyh209/Active-Directory/assets/33064730/dca7fc35-9d76-45a7-a457-7e57a3f48810)
![Settings_Network](https://github.com/johnnyh209/Active-Directory/assets/33064730/2d116317-5253-4c29-b7f8-da935a4e5c0d)

From there, I started up the virtual machine and ran through the installer for Windows Server 2019.

![Windows Server setup](https://github.com/johnnyh209/Active-Directory/assets/33064730/e866c922-feb5-4474-9bc6-4743f8771712)
![Windows Server setup part 2](https://github.com/johnnyh209/Active-Directory/assets/33064730/eabcc40d-4946-4364-9605-5a06006cd86f)
![Windows Server setup part 3](https://github.com/johnnyh209/Active-Directory/assets/33064730/4bfd140c-a461-4f09-9565-f4021b60097b)
![Windows Server Login](https://github.com/johnnyh209/Active-Directory/assets/33064730/214ef3ad-bf0f-4aa0-95a6-628150d00a0d)

Once Windows Server 2019 installation has completed and a local account has been made, I logged in with the local account credentials and `Server Manager` will open automatically. Below is a screenshot of the front page of Server Manager.

![Server Manager (Opens Automatically)](https://github.com/johnnyh209/Active-Directory/assets/33064730/f925596e-c0dd-45c8-90cd-d94f8f708b35)

**Step 7:** For consistency’s sake, I decided to rename this Windows Server 2019 system so that its name matches the name of the virtual machine assigned earlier during the virtual machine setup. I also figured that this would be a good opportunity to practice renaming the system. To do so, I used the following path: `Settings > System > About`. A quicker way is to `right-click the Windows logo > System`.

![Rename Server part 1](https://github.com/johnnyh209/Active-Directory/assets/33064730/557790e2-6bf3-4802-8ed1-a707437f630b)
![Rename Server part 2](https://github.com/johnnyh209/Active-Directory/assets/33064730/34a19f63-141d-42a1-a810-b1cb8bf18f30)



