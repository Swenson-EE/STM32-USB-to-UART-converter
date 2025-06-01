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
| Standard               | Speed   | Supported Connectors              | Max Cable Length            | Power |
|------------------------|---------|-----------------------------------|-----------------------------|-------|
| USB 2.0 Standard       | 480Mbps | All                               | 5 m                         | 15 W  |
| USB 3.2 Standard       | 5 Gbps  | USB 3 USB-A,  USB 3 USB-B,  USB-C | 3 m                         | 15 W  |
| USB 3.2 (Generation2)  | 10 Gbps | USB 3 USB-A, USB 3 USB-B, USB-C   | 1 m                         | 100 W |
| USB 3.2 Generation 2x2 | 20 Gbps | USB-C                             | 1 m                         | 100 W |
| Thunderbolt 3 Standard | 40 Gbps | USB-C                             | 2m - active, 0.8m - passive | 100 W |
| USB 4 (Thunderbolt 4)  | 40 Gbps | USB-C                             | 2m - active, 0.8m - passive | 100 W |

## USB Protocol Timing Diagram
![USB Protocol Timing Diagram](https://www.elprocus.com/wp-content/uploads/USB-Timing-Diagram.jpg)

**USB Protocol Timing Diagram**
> Image Credit: [USB Protocol : Architecture, Working, Synchronisation, DataFormat & Its Applications](https://www.elprocus.com/usb-protocol/)


The USB protocol uses a Non-Return to Zero Invert (NRZI) encoding to transmit data. This encoding represents a '1' by no change in the line state, and a '0' by a change in the line state. 

## USB Data Form
The Host USB starts all communication that happens on the USB bus. The data transmitted between the devices is called 'packets'. 

## Message Format
![USB Message Format](https://www.elprocus.com/wp-content/uploads/Message-Format-Diagram-of-USB.jpg)

**USB Message Format**
> Image Credit: [USB Protocol : Architecture, Working, Synchronisation, DataFormat & Its Applications](https://www.elprocus.com/usb-protocol/)

Data is transmitted LSB first. There are four main types of packets:
- Token
- Data
- Handshake
- Start of Frame

### Sync
The sync field is typically used to synchronize the transmitter and receiver to the same speed. 
- In a slow or high-speed system, the field includes 3 KJ pairs, which are followed through 2 K's to frame 8-bits of data.
- In a Hi-speed system, the sync needs 15 KJ pairs followed through 2 K's to frame 32 bits of data.
- The final 2-bits indicate where the Packet Identifier Field (PID field) begins.

### Packet Identifier Field (PID)
Used to specify the packet type being transmitted, which in turn tells the packet data format. The field is 8 bits long where the upper 4 bits denote the kind of packet and the lower 4 bits are the bit-wise complement of the upper 4 bits.

| Group     | PID Value | Packet Identifier      |
|-----------|-----------|------------------------|
| Token     | 0001      | OUT Token              |
|           | 1001      | IN Token               |
|           | 0101      | SOF Token              |
|           | 1101      | SETUP Token            |
| Data      | 0011      | DATA0                  |
|           | 1011      | DATA1                  |
|           | 0111      | DATA2                  |
|           | 1111      | MDATA                  |
| Handshake | 0010      | ACK Handshake          |
|           | 1010      | NAK Handshake          |
|           | 1110      | STALL Handshake        |
|           | 0110      | NYET (No Response Yet) |
| Special   | 1100      | PREamble               |
|           | 1100      | ERR                    |
|           | 1000      | Split                  |
|           | 0100      | Ping                   |


| PID<sub>0</sub> | PID<sub>1</sub> | PID<sub>2</sub> | PID<sub>3</sub> | nPID<sub>0</sub> | nPID<sub>1</sub> | nPID<sub>2</sub> | nPID<sub>3</sub> |
|--------|--------|--------|--------|---------|---------|---------|---------|


### Address Field
Indicates which device the packet is designated for. It is 7 bits long, and allows support of 127 devices.
- The zero address is not a valid device address, as any device which is not allocated an address reacts to transmitted packets from the zero address.

### Endpoint Field
The endpoint protocol is 4 bits in lenth and is used for extra addressing. Endpoints are optional and are used for transferring unidirectional data. These are either specified IN (Device to Host) or OUT (Host to Device). Endpoint 0 is a special endpoint known as the CONTROL endpoint, which each device is required to have. 

### Data Field
The length of the data field is not fixed, and can range from 0 to 8192 bits in length; and this always needs needs to be an integral number of bytes.

### CRC Field
Cyclic Redundancy Checks (CRC) are included with each packet payload where:
- Token packets include a 5-bit CRC
- Data packets include a 16-bit CRC

### EOP Field
Every packet terminates with a EOP (End of Packet). This includes a singled-ended zero (SE0) for 2 bit-lengths, followed by a J for 1 bit-length.


## Packet Types
### Token Packets
* **In** - Informs the USB device that the host wants to read information.
* **Out** - Informs the USB device that the host wants to send information.
* **Setup** - Used the begin control transfers.

| Sync | PID | ADDR | ENDP | CRC5 | EOP |
|------|-----|------|------|------|-----|

### Data Packets
* **Data0**
* **Data1**

High speed mode also offers DATA2 and MDATA.

| Sync | PID | Data | CRC16 | EOP |
|------|-----|------|-------|-----|

### Handshake Packets
* **ACK** - Acknowledge that the packet was successfully received.
* **NAK** - Reports that the device temporarily cannot send or receive data. Also used during interrupt transactions to inform the host there is no data to send.
* **STALL** - The device is in a state that it requires intervention from the host.

| Sync | PID | EOP |
|------|-----|-----|

### Start of Frame Packets
A 11-bit frame number send by the host ever 1ms +- 500ns on a full speed bus or every 125 us +- 0.0625 us on a high speed bus.

| Sync | PID | Frame Number | CRC5 | EOP |
|------|-----|--------------|------|-----|




## References
- *USB Protocol : Architecture, Working, Synchronisation, DataFormat & Its Applications* ElProCus. Available at: [USB Protocol : Architecture, Working, Synchronisation, DataFormat & Its Applications](https://www.elprocus.com/usb-protocol/). Accessed on May 31, 2025.

- Amanpreet Singh. *Signal and Encoding of USB System (Part 5/6)* Engineers Garage. Published May 20, 2025. Available at: [Signal and Encoding of USB System (Part 5/6)](https://www.engineersgarage.com/signal-and-encoding-of-usb-system-part-5-6/). Accessed on May 31, 2025.
