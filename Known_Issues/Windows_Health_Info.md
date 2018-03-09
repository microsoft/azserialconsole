## Issue ##
When trying to use Azure Serial Console to connect to a Windows virtual machine you receive VM health information similar to the example below, but the VM does not respond to pressing enter or other input.

```
======== Microsoft Azure VM Health Report - Start 2018-03-06T02:06:40.6256349Z ========
{"reportTime":"2018-03-06T02:06:29.0389712Z","networkAdapters":[{"name":"Ethernet 2","status":"Up","macAddress":"00-0F-3A-A7-71-D0","ipProperties":[{"protocolVersion":4,"address":"10.0.1.4","isDhcpEnabled":true},{"protocolVersion":6,"address":"fe80::90e7:17ff:1ab5:522d%13","isDhcpEnabled":false}]},{"name":"Loopback Pseudo-Interface 1","status":"Up","macAddress":"","
...
```

## Cause ##
This issue occurs when the Special Administrative Console (SAC) has not been enabled on the virtual machine.

## More Info ##
Windows virtual machines in Azure with a current VM agent will emit health information through the serial port when SAC is _not_ enabled. When processed, this health information can be useful in diagnosing remote desktop connectivity and other issues with the guest VM. However this information is output-only; since the SAC is not enabled, the VM will not respond to input from the Azure serial console. 


## Resolution ##
To administer this Windows VM using Azure Serial Console, use the steps [here](../Azure-virtual-machine-serial-console.md#accessing-serial-console-for-windows) to enable the Special Administrative Console (SAC).