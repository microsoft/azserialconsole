## Non-Maskable Interrupt (NMI) ##
A non-maskable interrupt(NMI) is designed to create a signal that sofware on a virtual machine will not ignore. Historically, NMIs have been used to monitor for hardware issues on systems that required specific response times.  Today, programmers and system administrators often use NMI as a mechanism to debug or troubleshoot systems which are hung.

The Serial Console can be used to send an NMI to an Azure virtual machine. Once the NMI is delivered, the virtual machine configuration will control how the system respond.  Both Windows and Linux operating systems can be configured to crash and create a memory dump when receiving an NMI.

### Windows ###
For information on configuring Windows to create a crash dump when it receives an NMI, see: [How to generate a complete crash dump file or a kernel crash dump file by using an NMI on a Windows-based system](https://support.microsoft.com/en-us/help/927069/how-to-generate-a-complete-crash-dump-file-or-a-kernel-crash-dump-file)

### Linux ###
For information on configuring Linux to create a crash dump when it receives an NMI, including `unknown_nmi_panic`, `panic_on_io_nmi`, and `panic_on_unrecovered_nmi`, see: [Documentation for /proc/sys/kernel/*](https://www.kernel.org/doc/Documentation/sysctl/kernel.txt) and the distribution specific documentation below:
 
 #### Ubuntu ####
 - [Kernel Crash Dump](https://help.ubuntu.com/lts/serverguide/kernel-crash-dump.html)

 #### Red Hat ####
 - [What is an NMI and what can I use it for?](https://access.redhat.com/solutions/4127)
 - [How can I configure my system to crash when NMI switch is pushed?](https://access.redhat.com/solutions/125103)
 - [Crash Dump Admin Guide](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/pdf/kernel_crash_dump_guide/kernel-crash-dump-guide.pdf)

#### SUSE ####
- [Configure kernel core dump capture](https://www.suse.com/support/kb/doc/?id=3374462)
#### CoreOS ####
- [Collecting crash logs](https://coreos.com/os/docs/latest/collecting-crash-logs.html)


### Known Issues ###
- *If the serial console connection is open for several minutes without sending either a [SysRq](sysrq.md) or [NMI](nmi.md), attempts to send a [SysRq](sysrq.md) or [NMI](nmi.md) may not initially return a response and cause a console error after several seconds.*
- *If the the virtual machine is rebooted in the same session, attempts to send a [SysRq](sysrq.md) or [NMI](nmi.md) may fail after the serial console session reconnection.*