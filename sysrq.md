## System Request (SysRq) ##
A SysRq is a sequence of keys understood by the Linux operation system kernel which can trigger a set of pre-defined actions. These commands are often used when virtual machine troubleshooting or recovery can not be performed through traditional administration (for example the VM is hung). Using the SysRq feature of Azure Serial Console will mimic pressing of the SysRq key and characters entered on a physical keyboard.

Once the SysRq sequence is delivered, the kernel configuration will control how the system responds. For information on enabling and disabling SysRq, see the SysRq Admin Guide [text](https://www.kernel.org/doc/Documentation/admin-guide/sysrq.rst) | [markdown](https://github.com/torvalds/linux/blob/master/Documentation/admin-guide/sysrq.rst).  Links to additional distribution specific documentation can be found below.

The Azure Serial Console SysRq user interface will accept a sequence of SysRq commands entered into the dialog.  This allows for series of SysRq's to perform a high-level operation such as a safe reboot using: `REISUB`.

![](../images/sysreq_UI.jpg)

The SysRq command cannot be used on virtual machines that are stopped or whose kernel is in a non-responsive state. (for example a kernel panic).

### Command Keys ###
From the SysRq Admin Guide above:

|Command| Function
| ------| ----------- |
|``b``  |   Will immediately reboot the system without syncing or unmounting your disks.
|``c``  |   Will perform a system crash by a NULL pointer dereference. A crashdump will be taken if configured.
|``d``  |   Shows all locks that are held.
|``e``  |   Send a SIGTERM to all processes, except for init.
|``f``  |   Will call the oom killer to kill a memory hog process, but do not panic if nothing can be killed.
|``g``  |   Used by kgdb (kernel debugger)
|``h``  |   Will display help (actually any other key than those listed here will display help. but ``h`` is easy to remember :-)
|``i``  |    Send a SIGKILL to all processes, except for init.
|``j``  |    Forcibly "Just thaw it" - filesystems frozen by the FIFREEZE ioctl.
|``k``  |    Secure Access Key (SAK) Kills all programs on the current virtual console. NOTE: See important comments below in SAK section.
|``l``  |    Shows a stack backtrace for all active CPUs.
|``m``  |    Will dump current memory info to your console.
|``n``  |    Used to make RT tasks nice-able
|``o``  |    Will shut your system off (if configured and supported).
|``p``  |    Will dump the current registers and flags to your console.
|``q``  |    Will dump per CPU lists of all armed hrtimers (but NOT regular timer_list timers) and detailed information about all clockevent devices.
|``r``  |    Turns off keyboard raw mode and sets it to XLATE.
|``s``  |    Will attempt to sync all mounted filesystems.
|``t``  |    Will dump a list of current tasks and their information to your console.
|``u``  |    Will attempt to remount all mounted filesystems read-only.
|``v``  |    Forcefully restores framebuffer console
|``v``  |    Causes ETM buffer dump [ARM-specific]
|``w``  |    Dumps tasks that are in uninterruptable (blocked) state.
|``x``  |    Used by xmon interface on ppc/powerpc platforms. Show global PMU Registers on sparc64. Dump all TLB entries on MIPS.
|``y``  |    Show global CPU Registers [SPARC-64 specific]
|``z``  |    Dump the ftrace buffer
|``0``-``9`` | Sets the console log level, controlling which kernel messages will be printed to your console. (``0``, for example would make it so that only emergency messages like PANICs or OOPSes would make it to your console.)

### Distribution-specific documentation ###
#### Ubuntu ####
 - [Kernel Crash Dump](https://help.ubuntu.com/lts/serverguide/kernel-crash-dump.html)
#### Red Hat ####
- [What is the SysRq Facility and how do I use it?](https://access.redhat.com/articles/231663)
- [How to use the SysRq facility to collect information from a RHEL server](https://access.redhat.com/solutions/2023)
#### SUSE ####
- [Configure kernel core dump capture](https://www.suse.com/support/kb/doc/?id=3374462)
#### CoreOS ####
- [Collecting crash logs](https://coreos.com/os/docs/latest/collecting-crash-logs.html)

### Known Issues ###
- *If the serial console connection is open for several minutes without sending either a [SysRq](sysrq.md) or [NMI](nmi.md), attempts to send a [SysRq](sysrq.md) or [NMI](nmi.md) may not initially return a response and cause a console error after several seconds.*
- *If the the virtual machine is rebooted in the same session, attempts to send a [SysRq](sysrq.md) or [NMI](nmi.md) may fail after the serial console session reconnection.*