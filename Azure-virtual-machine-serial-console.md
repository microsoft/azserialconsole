# Azure's Virtual Machine Serial Console -- Early Access Preview (ONLY AVAILABLE IN WEST CENTRAL US REGION)

> [!NOTE] 
> Previews are made available to you on the condition that you agree to the terms of use. For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews.] (https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/)
> ACCESS VIA SERIAL CONSOLE SHOULD BE LIMITED TO DEV-TEST VIRTUAL MACHINES. WE STRONGLY RECOMMEND NOT TO USE THIS FOR ANY PRODUCTION VIRTUAL MACHINE.
>

Azure's Virtual Machine Serial Console provides access to serial console for your Linux and Windows Virtual Machines on Azure. This Serial connection is to COM1 serial port of your Virtual Machine and provides access to the Virtual Machine regardless of that Virtual Machine's network / operating system state. Access to Serial Console for a Virtual Machine can be done only via Azure Portal and for those who have VM Contributor or above access. 

### Important information
Currently this service is in **preview** and access to Serial Console for the Virtual Machine is limited to white-listed subscriptions who participated in early access preview and for Virtual Machines available in West Central US region.


## Accessing Serial Console

Serial Console for a Virutal Machine is only access via [Azure portal](https://portal.azure.com). Below are the steps to access Serial Console for a Virtual Machine via portal 

1. Open the Virtual Machine that you want to access in Azure Portal 
2. Scroll down onto the Support + Troubleshooting section 
3. Click in Serial Console (Preview) to access serial console 

![](https://github.com/Microsoft/azserialconsole/blob/master/images/SerialConsole-LinuxAccess.gif)

> [!NOTE] 
> Only subscriptions that are whitelisted as a part of early access preview will be able to see Serial Console section in the portal. Please also note that serial console requires local user with password configured. At this VMs only configured with public key wont have access to serial console. To create a local user with password follow [VM Access Extension](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/using-vmaccess-extension) to create local user with password.

## Serial Console  Security 

### Access Security 
Access to Serial console is limited to users who have [VM Contributors](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-built-in-roles#virtual-machine-contributor) or above access to the Virtual Machine. If your AAD tenant requires Multi-Factor Authentication then access to serial console will also need MFA as its access is via [Azure Portal](https://portal.azure.com).

### Channel Security

All data is sent back and forth is encrypted on the wire.

### Audit logs

All access to Serial Console are currently logged in the [boot diagnostics](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/boot-diagnostics) logs of the virtual machine. Access to these logs are owned and controlled by the Virtual Machine Administrator.  

>[!CAUTION] While no access passwords for the console are logged. However if commands run within a the console contains passwords/secrets those will be logged in the Virtual Machine boot diagnostics logs. No body other than readers of diagnostics storage account have access to these, however we recommend following the best practice of using SSH console for all secerts related work. 

## Common Scenarios for accessing Serial Console 

Scenario          | Actions in Serial Console                |  OS Applicability 
------------------|:----------------------------------------:|------------------:
Broken FSTAB file | Enter key to continue and fix fstab file | Linux 
Incorrect Firewall rules | Access Serial Console and fix iptables/Windows firewall rules | Linux/Windows 
Filesystem corruption/check | Access Serial Console and recover filesytem | Linux/Windows 
SSH/RDP configuration issues | Access Serial Console and change settngs | Linux/Windows 
Network lock down system| Access Serial Console via portal to manage system | Linux/Windows 
Interacting with bootloader | Access GRUB/BCD via serial console | Linux/Windows 

## Accessing Serial Console for Linux ( Distro Specific Scenarios ) 

Most [Endorsed Azure Linux Distributions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/endorsed-distros) have serial console configured by default. Just by clicking in the portal on the Serial console section will provide access to the console. 

### Access for RedHat 

RedHat Images available on Azure has Serial Console enabled by default. Single User Mode in Red Hat requires root user to be enabled, which is by default disabled. If you have a need to enable Single user mode , use the following instructions 

1. Login to the Red Hat system via SSH
2. Enable password for root user 
 * passwd root ( set a strong root password )
3. Ensure root user can only login via ttyS0
 * edit /etc/ssh/sshd_config and ensure PermitRootLogin is set to no
 * edit /etc/securetty file to only allow logins via ttyS0 

Now if the system boots into single user mode you can login via root password.

### Access for Ubuntu 

Ubuntu Images available on Azure has Serial Console enabled by default. If the system boots into Single user mode you can access without additional credentials. 

### Access for CoreOS

CoreOS Images available on Azure has Serial Console enabled by default. If required system can be booted into Single user mode via changing GRUB parameters and adding coreos.autologin=ttyS0 would enable core user to login and available in Serial Console. 

### Access for SUSE

SLES Images available on Azure currently does not have Serial Console enabled by default. To enable Serial Console on SLES please follow the [KB article](https://www.novell.com/support/kb/doc.php?id=3456486). 


### Access for CentOS

CentOS Images available on Azure has Serial Console enabled by default. For Single user mode please follow instructions similar to Red Hat Images above. 

### Access for Oracle Linux

Oracle Linux Images available on Azure has Serial Console enabled by default. For Single user mode please follow instructions similar to Red Hat Images above.

### Access for Custom Linux Image

To enable Serial Console for your Custom Linux VM Image, enable console in inittab to run a terminal on ttyS0. Below is an example to add in inittab file 

S0:12345:respawn:/sbin/agetty -L 115200 console vt102  

## Accessing Serial Console for Windows 

Windows Images on Azure does not have [Special Administrative Console](https://technet.microsoft.com/en-us/library/cc787940(v=ws.10).aspx) (SAC) enabled by default. To enable Serial console for Windows Virtual Machines please the following steps 

1. Connect to your Windows Virtual Machine via Remote Desktop
2. From an Administrative command prompt run the following commands 
* bcdedit /ems {current} on
* bcdedit /emssettings EMSPORT:1 EMSBAUDRATE:115200
3. Reboot the system for the SAC console to be enabled

![](https://github.com/Microsoft/azserialconsole/blob/master/images/SerialConsole-PrivatePreviewWindows.gif)

## Errors



## Availability 
The current Preview is available in **West US Central** Region of Azure. 


## FAQ

## Next Steps

Learn more about bootdiagnostics