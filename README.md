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

**Step 6:** For consistency’s sake, I decided to rename this Windows Server 2019 system so that its name matches the name of the virtual machine assigned earlier during the virtual machine setup. I also figured that this would be a good opportunity to practice renaming the system. To do so, I used the following path: `Settings > System > About`. A quicker way is to `right-click the Windows logo > System`.

![Rename Server part 1](https://github.com/johnnyh209/Active-Directory/assets/33064730/557790e2-6bf3-4802-8ed1-a707437f630b)
![Rename Server part 2](https://github.com/johnnyh209/Active-Directory/assets/33064730/34a19f63-141d-42a1-a810-b1cb8bf18f30)

**Step 7:** Now that the menial tasks are completed, this next step will be where I configure Active Directory Domain Services (AD DS). To do so, I clicked on Manage in the top-right corner, then clicked on `Add Roles and Features`. The installation wizard will open up. I simply clicked `Next` until I reached the `Server Roles` page of the wizard because no changes needed to be made in any of the previous pages. In this `Server Roles` page, I checked the box for `Active Directory Domain Services` to add this feature. From here, I kept clicking “Next” until I reached the end of the wizard and waited for the installation to finish. At this point, AD DS has been enabled. 

![Configure AD DS Part 1](https://github.com/johnnyh209/Active-Directory/assets/33064730/5320a2a1-38ab-48c7-812f-db47fc8d538c)
![Configure AD DS Part 4](https://github.com/johnnyh209/Active-Directory/assets/33064730/4503bb3a-c5c2-4b72-9f72-ed0212051f1f)
![Configure AD DS Part 5](https://github.com/johnnyh209/Active-Directory/assets/33064730/e2defb19-659d-42ed-a6b3-a083d51e8b9b)

**Step 8:** With AD DS setup, we need to `Promote this server to a domain controller`. As the domain controller, this Windows Server system will be able to manage all of the computers and users that will be connected to this Windows domain network. The domain controller also manages authentication/verification of users. 

![Configure AD DS Part 7](https://github.com/johnnyh209/Active-Directory/assets/33064730/202624f5-a15a-41b0-9344-713feb151b5b)

In the first page of the configuration wizard, I selected `Add a new forest` and input a domain address in the text box labeled `Domain`. For this project, I used laborg.local. Then hit next. The following page will ask for a password; click next after coming up with a password. 

![Configure Domain Controller part 1](https://github.com/johnnyh209/Active-Directory/assets/33064730/f00dc437-f9c7-4eb2-8c6b-ee57cdb4c368)
![Configure Domain Controller part 2](https://github.com/johnnyh209/Active-Directory/assets/33064730/aaeb2057-17f0-4ab3-b603-50671becf9f6)

This next page will have a message at the top with the yellow triangle containing a black exclamation mark symbol that says `A delegation for this DNS server cannot be created because of the authoritative parent zone…` We can ignore this because a DNS will be chosen automatically. 

![Configure Domain Controller part 3](https://github.com/johnnyh209/Active-Directory/assets/33064730/95a3b6e6-a74f-41b6-9f5d-4473bb3d7ea6)

In the `Additional Options` page, we will be provided a NetBIOS domain name. You are welcome to change it, but I decided to keep the already entered name. This part should be the last thing that I needed to make any changes or input any information into. I just went through the remaining pages of the configuration wizard and clicked `Install`.  The system will need to be restarted after the install completes.

![Configure Domain Controller part 4](https://github.com/johnnyh209/Active-Directory/assets/33064730/97369324-f17a-4750-89c5-152d2711e002)
![Configure Domain Controller part 5](https://github.com/johnnyh209/Active-Directory/assets/33064730/ad48e0cb-845c-4853-b7b3-bfd657d07006)
![Configure Domain Controller part 6 (Restarting)](https://github.com/johnnyh209/Active-Directory/assets/33064730/53271d19-2f6c-4e5b-b02d-cc53a234852e)

**Step 9:** By this stage, the Windows Server 2019 virtual machine is all set up. Next, we will be creating virtual machines for Windows 10 Enterprise. For the purpose of this project, I will be creating two virtual machines: one for a help desk employee and one for a regular employee. I started off creating the virtual machine for the help desk employee first. The process to create the Windows 10 virtual machines will be the same as what I did when creating the Windows Server 2019 virtual machine. 

![Windows 10 Installation Part 2](https://github.com/johnnyh209/Active-Directory/assets/33064730/626effc9-a949-49b0-893d-dd10a37aaf4e)
![Windows 10 Installation Part 4](https://github.com/johnnyh209/Active-Directory/assets/33064730/10d29fea-b1f9-4290-aed2-f95d0cecf2b2)

Once I have created the help desk virtual machine, I performed a full clone of the Windows 10 Virtual machine. 

![Clone](https://github.com/johnnyh209/Active-Directory/assets/33064730/7f4a3b38-2fed-4127-95fc-c53de867b9ad)
![Clone Part 2](https://github.com/johnnyh209/Active-Directory/assets/33064730/b4a17341-4805-45d4-985a-96557727e7f1)

One of the Windows 10 system will be for an imaginary member of an IT help desk, and one will be for a regular employee.

**Step 10:** After completing the setup of the two Windows 10 virtual machines, it is time to add them to the Active Directory. In this step, I will have all 3 virtual machines running at the same time for easier management and workflow. Let’s start off with adding the `HelpDesk` virtual machine first. 

First, on the Windows Server 2019 virtual machine in Server Manager, I navigated to `Tools > Active Directory Users and Computers`. This opened up the Active Directory Users and Computers window. On the left hand column, we expanded the `laborg.local` domain. Several directories will be listed that are within the `laborg.local` domain. We then went into the `Users` directory, right-clicked on that directory, hovered over `New`, and clicked on `User`. This is to create a new user. 

![Add HelpDesk to DS Part 1](https://github.com/johnnyh209/Active-Directory/assets/33064730/3c7be7a4-b51e-44bb-8261-036271ec6b51)

We will be creating a new user for the help desk account. 

![Add HelpDesk to DS Part 2](https://github.com/johnnyh209/Active-Directory/assets/33064730/210ba8c3-709c-4888-9c7d-c2aa896f9658)
![Add HelpDesk to DS Part 3](https://github.com/johnnyh209/Active-Directory/assets/33064730/cade1d59-442d-4080-b5ec-e209b56f97d2)

After creating this help desk user, it should be listed in the `Users directory`. I then right-clicked on `HelpDesk LabOrg` user, went to `Properties`, and clicked on the `Member Of` tab. This is where we will make `HelpDesk LabOrg` an administrator account. Click on `Add…` and in the text box type in `Domain Admins`. A new entry with the name `Domain Admins` will be added. Click on it to highlight it, and then click on the `Apply` button below.

![Make HelpDesk Admin Account Part 1](https://github.com/johnnyh209/Active-Directory/assets/33064730/cb5d6a28-4670-4a9b-b80b-2649f38b87fb)
![Make HelpDesk Admin Account Part 2](https://github.com/johnnyh209/Active-Directory/assets/33064730/54478e0d-5b98-41c7-88bb-e8623dad089d)

**Step 11:** At this stage, I will be adding the `HelpDesk` system to the domain. I went into the `HelpDesk` virtual machine and navigated through the following: `Start > Settings > System > About > Advanced system settings`. This opened up the `System Properties`. In the `Computer Name` tab in System Properties, I clicked on `Change…` which opened up `Computer Name/Domain Changes`. Here, I selected `Domain` and entered the domain name. For me, it will be `LabOrg`.

![Add HelpDesk to Domain Part 1](https://github.com/johnnyh209/Active-Directory/assets/33064730/77be3da2-fa02-4c08-a3b1-7ce685f3c28a)

When I clicked `ok`, however, I was presented with the following error:

![Add HelpDesk to Domain Part 2 (Error)](https://github.com/johnnyh209/Active-Directory/assets/33064730/b803aa6e-2148-4aab-b496-764da754b754)

This means that the `HelpDesk` virtual machine could not find/connect to our Windows Server 2019. In a production environment, I probably wouldn’t encounter this error. Because we are in a virtual environment, we will have to configure everything manually. This should be a simple fix. First, I went to my Windows Server 2019 virtual machine, opened up `CMD`, and entered in the command: `ipconfig /all`. This will provide me with the IP address of the domain controller (the Windows Server 2019 virtual machine). 

![Add HelpDesk to Domain Part 3 (Fix Error)](https://github.com/johnnyh209/Active-Directory/assets/33064730/de1badfd-5e77-406b-a5c2-63dd21ae1890)

Then, I moved back to the HelpDesk virtual machine. Went to `Settings > Network & Internet > Status > Change adapter options`. This showed me the network adapter(s) for the system. I right-clicked on the network adapter, and clicked on `Properties`. Then, I selected `Internet Protocol Version 4`, and clicked on `Properties`. In the DNS section of the IPv4 properties page, I entered the domain controller ip address into the `Preferred DNS server` text box and clicked `OK` to close the IPv4 Properties window. I then clicked `OK` one more time to close the network adapter properties window. 

![Add HelpDesk to Domain Part 4 (Fix Error)](https://github.com/johnnyh209/Active-Directory/assets/33064730/81261a69-24e9-4455-8984-3abacf598d15)

I then went back to the `Computer Name/Domain Changes` window, and tried to add the HelpDesk machine to the active directory again. This time, it worked and a new window opened, asking me to input the name and password of the user that I created in step 10 rather than the local account when I set up this Windows 10. For me, this will be the user that I named `HelpDesk LabOrg`. This will successfully add the HelpDesk Windows 10 virtual machine into the active directory. 

![Add HelpDesk to Domain Part 5 (Fixed Error)](https://github.com/johnnyh209/Active-Directory/assets/33064730/76a1b78a-562e-4140-9c6d-37a623626d4a)
![Add HelpDesk to Domain Part 5 (Success)](https://github.com/johnnyh209/Active-Directory/assets/33064730/4c1a6196-cba0-4609-bcaf-f2593baf600f)

At the login screen, I saw on the lower left hand corner the local account listed, and an option for `Other user`. I used `Other user`, and entered in the credentials for the HelpDesk LabOrg I created in the active directory to log in. 

![Add HelpDesk to Domain Part 8 (Confirmation)](https://github.com/johnnyh209/Active-Directory/assets/33064730/a4a57153-3adc-44eb-ac89-32746287c940)

**Step 13:** To add the `Staff` Windows 10 virtual machine to the active directory, we followed the same steps that we did to add the HelpDesk Windows 10 virtual machine to the active directory.

![Adding Staff to Domain part 3 (Confirmation)](https://github.com/johnnyh209/Active-Directory/assets/33064730/8e28022e-8b85-4492-84f5-87c94c9842b5)

Successfully adding the `Staff` system to the active directory concludes this project.
