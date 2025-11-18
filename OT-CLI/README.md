| Supported Targets | ESP32-C5 | ESP32-C6 | ESP32-H2 |
| ----------------- | -------- | -------- | -------- |

# OpenThread Command Line Example

This example demonstrates an [OpenThread CLI](https://github.com/openthread/openthread/blob/master/src/cli/README.md), with some additional features such as TCP, UDP and Iperf.

## How to use example

### Hardware Required

To run this example, a board with IEEE 802.15.4 module (for example ESP32-H2) is required.

### ⚙️ Configure the project

```
idf.py menuconfig
```

The example can run with the default configuration. OpenThread Command Line is enabled with UART as the default interface. Additionally, USB JTAG is also supported and can be activated through the menuconfig:

```
Component config → ESP System Settings → Channel for console output → USB Serial/JTAG Controller
```

### 🚀 Build, Flash, and Run

Build the project and flash it to the board, then run monitor tool to view serial output:

```
idf.py -p PORT build flash monitor
```

Now you'll get an OpenThread command line shell.

### 🖥️ Example Output

The `help` command will print all of the supported commands.
```bash
>  help
I(7058) OPENTHREAD:[INFO]-CLI-----: execute command: help
bbr
bufferinfo
ccathreshold
channel
child
childip
childmax
childsupervision
childtimeout
coap
contextreusedelay
counters
dataset
delaytimermin
diag
discover
dns
domainname
eidcache
eui64
extaddr
extpanid
factoryreset
...
```

## 📶 Set Up Network

To run this example, at least two ESP32-H2 boards flashed with this ot_cli example are required.

On the first device, run the following commands:
```bash
> factoryreset
... # the device will reboot

> dataset init new
Done
> dataset commit active
Done
> ifconfig up
Done
> thread start
Done

# After some seconds

> state
leader
Done
```
Now the first device has formed a Thread network as a leader. Get some information which will be used in next steps:
```bash
> ipaddr
fdde:ad00:beef:0:0:ff:fe00:fc00
fdde:ad00:beef:0:0:ff:fe00:8000
fdde:ad00:beef:0:a7c6:6311:9c8c:271b
fe80:0:0:0:5c27:a723:7115:c8f8

# Get the Active Dataset
> dataset active -x
0e080000000000010000000300001835060004001fffe00208fe7bb701f5f1125d0708fd75cbde7c6647bd0510b3914792d44f45b6c7d76eb9306eec94030f4f70656e5468726561642d35383332010258320410e35c581af5029b054fc904a24c2b27700c0402a0fff8
```

On the second device, set the active dataset from leader, and start Thread interface:
```bash
> factoryreset
... # the device will reboot

> dataset set active 0e080000000000010000000300001835060004001fffe00208fe7bb701f5f1125d0708fd75cbde7c6647bd0510b3914792d44f45b6c7d76eb9306eec94030f4f70656e5468726561642d35383332010258320410e35c581af5029b054fc904a24c2b27700c0402a0fff8
> ifconfig up
Done
> thread start
Done

# After some seconds

> state
child  # router is also a valid state
Done
```
The second device has joined the Thread network as a child (or a router).

## Extension commands

You can refer to the [extension command](https://github.com/espressif/esp-thread-br/blob/main/components/esp_ot_cli_extension/README.md) about the extension commands.

The following examples are supported by `ot_cli`:

* TCP and UDP Example
* Iperf Example

---

# Demo of sending messages between devices using TCP
  
You can also refer our [**Detailed Guide**](https://github.com/make2explore/ESP32-OpenThread-Command-Line-Example/tree/main/OT-CLI-TCP-UDP-demo) of demo of sending messages between devices using TCP and UDP with **flow diagrams** and **Topology**.
Please refer it for more details.

## Quick Guide
## For the First ESP OT-CLI device (Leader), open a TCP socket server

```bash
> tcpsockserver open
Done
```

### Create a new port with any 5 digits and bind it

```bash
> tcpsockserver bind :: 12345
Done
```

## On another ESP32 (Child), set up the TCP client  
### open client TCP socket  

```bash
> tcpsockclient open  
Done
```
  
### connect to server with on same port
Use IP which we copied in the last steps:

```bash
> tcpsockclient connect <IP> <Port>
```

Example:

```bash
> tcpsockclient connect fdde:ad00:beef:0:0:ff:fe00:fc00 12345
Done
```

## Send messages between the ESP32 devices

Send `"Hello"` from TCP Client to TCP Server:

```bash
> tcpsockclient send hello
Done
```

Send `"Hi"` from TCP Server to TCP Client:

```bash
> tcpsockserver send hi
Done
```

## Closing the TCP connection

On Client:
```bash
> tcpsockclient close
Done
```

On Server:
```bash
> tcpsockserver close
Done
```

---

ℹ️ If you want to communicate with another Thread device, you need to close the current TCP connection and create a new one.  
The existing Thread Network will still keep running.
