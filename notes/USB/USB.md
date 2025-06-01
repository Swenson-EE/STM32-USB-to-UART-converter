# USB Protocol
The USB protocol is a common communication protocol that is used for a host controller -- such as a smartphone or pc -- to communicate between different peripheral devices -- like keyboard and mouse, digital cameras, media devices, etc.

There are several different types of USB connectors available. Type A and Type B are the most frequently used USB connectors, however, the are being replaced by Mini-USB, Micro-USB, and USB-C cables.

## Pin Configuration
![Type A USB Connector Pin Configuration](https://www.elprocus.com/wp-content/uploads/Type-A-USB-Connector-Pin-Configuration.jpg)

**Type A USB Connector Pin Configuration**
> Image Credit: [USB Protocol : Architecture, Working, Synchronisation, DataFormat & Its Applications](https://www.elprocus.com/usb-protocol/)

- Pin 1 (VBUS)
    - Red colored wire, used for providing power supply.
- Pin 2 (D-)
    - White colored wire, used for a differential pair for connectivity of USB.
- Pin 3 (D+)
    - Green colored wire, used for a differential pair for connectivity of USB.
- Pin 4 (GND)
    - Black colored wire, used as a ground pin.

## USB Protocol Architecture
![USB Protocol Architecture](https://www.elprocus.com/wp-content/uploads/USB-Protocol-Architecture.jpg)

**Type A USB Connector Pin Configuration**
> Image Credit: [USB Protocol : Architecture, Working, Synchronisation, DataFormat & Its Applications](https://www.elprocus.com/usb-protocol/)

In the USB structure, every device makes a point-to-point connection to transmit data. I/O devices are connected to the Host through through a Hub. A hub is a connecting point between the I/O devices and the Host. There is a root hub which connects to the Host, and branches of Hubs that connect to each of the USB devices.

These I/O devices can be daisy-chained through a maximum of 5 Hubs.

A USB port can support up to a maximum of up to 127 devices.

## How does it work?
The USB protocol uses a polling principle, where the Host continously checks whether the I/O device is prepared for transmitting data or not. This puts the responsibility on the processor to check continuously.

A new device connected to a Hub is addressed. The Host polls the Hubs to obtain their condition to know which I/O devices are connected or disconnected. The Host then essentially interrogates the device through a process called Enumeration, to obtain information about its function, speed, and other characteristics. The host allocates an address to the new device which is written to the device register. This allows the host to automatically identify new I/O devices when one is connected and scan for capabilities. The USB protocol is also hot-pluggable, which means the I/O device can connect or disconnect to the host system without any shutdown or restart, as the system continously detects when the device is connected or disconnected. 

The protocol can also support isochronous traffic where data is transmitted at a preset interval of time. Isochronous data is very fast compared to synchronous and asynchronous data transfer. The root hub does this by transmitting a series of bits over USB which specifies the start of isochronous data, and the data can be transmitted after this series of bits. 


## USB Standards and Specifications
| Standard               | Speed   | Supported Connectors              | Max Cable Length           | Power |
|------------------------|---------|-----------------------------------|----------------------------|-------|
| USB 2.0 Standard       | 480Mbps | All                               | 5 m                        | 15 W  |
| USB 3.2 Standard       | 5 Gbps  | USB 3 USB-A,  USB 3 USB-B,  USB-C | 3 m                        | 15 W  |
| USB 3.2 (Generation2)  | 10 Gbps | USB 3 USB-A, USB 3 USB-B, USB-C   | 1 m                        | 100 W |
| USB 3.2 Generation 2x2 | 20 Gbps | USB-C                             | 1 m                        | 100 W |
| Thunderbolt 3 Standard | 40 Gbps | USB-C                             | 2m - active 0.8m - passive | 100 W |
| USB 4 (Thunderbolt 4)  | 40 Gbps | USB-C                             | 2m - active 0.8m - passive | 100 W |

## USB Protocol Timing Diagram
The USB protocol uses a Non-Return to Zero Invert (NRZI) encoding to transmit data. This encoding represents a '1' by no change in the line state, and a '0' by a change in the line state. 



## References


https://www.elprocus.com/usb-protocol/

https://www.engineersgarage.com/signal-and-encoding-of-usb-system-part-5-6/ 



