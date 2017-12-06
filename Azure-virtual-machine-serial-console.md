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

## Accessing Serial Console for Linux ( Distro Specific Scenarios ) 

### Access for RedHat 

### Access for Ubuntu 

### Access for CoreOS

### Access for SUSE 

### Access for CentOS

### Access for Oracle Linux

### Access for Custom Linux Image


## Accessing Serial Console for Windows 


## Errors

### Examples

## Availability 
The current Preview is available in **West US Central** Region of Azure. 


## FAQ

## Next Steps

Learn more about bootdiagnostics