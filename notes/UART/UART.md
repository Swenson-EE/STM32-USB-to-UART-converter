# UART Protocol
UART -- Universal Asynchronous Receiver-Transmitter -- is a very common device-to-device communication protocol. During serial communication, data is transferred bit-by-bit using a single line. Which can be extended to two lines for two-way communication. 

## Interface
![Two UART Communication Interface](https://www.analog.com/en/_/media/images/analog-dialogue/en/volume-54/number-4/articles/uart-a-hardware-communication-protocol/335962-fig-01.svg?w=900&rev=a39d7f916b404552967cc0579b7c0639, "Source: Analog Devices UART article")
**Two-Way UART Communication**
> Image Credit: [UART: A Hardware Communication Protocol Understanding Universal Asynchronous Receiver/Transmitter
](https://www.analog.com/en/resources/analog-dialogue/articles/uart-a-hardware-communication-protocol.html#:~:text=By%20definition%2C%20UART%20is%20a,going%20to%20the%20receiving%20end.)

The two signals used in UART devices are:
- TX (Transmitter)
- RX (Receiver)

UART has many different configurations within operating such as: speed, data frame, parity bits, and stop bits.

## Data transmission
![UART Packet](https://www.analog.com/en/_/media/images/analog-dialogue/en/volume-54/number-4/articles/uart-a-hardware-communication-protocol/335962-fig-03.svg?w=900&rev=ad33a0f741fd40a79887152fcf0b7944, "Source: Analog Devices UART article")
**UART Packet**
> Image Credit: [UART: A Hardware Communication Protocol Understanding Universal Asynchronous Receiver/Transmitter
](https://www.analog.com/en/resources/analog-dialogue/articles/uart-a-hardware-communication-protocol.html#:~:text=By%20definition%2C%20UART%20is%20a,going%20to%20the%20receiving%20end.)


### Start bit
UART is typically held high when not transmitting data. To start a transmission, the transmitting UART line pulls the TX line from high to low for 1 clock cycle. The receiving UART detects this high to low transition and can begin reading the data frame at the agreed upon baud rate.

### Data frame
The data frame is the actual data being transferred. This can be 5 bits to 8 bits long if parity is used, and if parity is not used, then the data frame can be 9 bits long. Data is typically sent with the least significant bit (LSB) first.

### Parity
Parity is the evenness or oddness of the number. This is a way to tell if any data changed during transmittion. The number of bits with a value of 1 are counted and is checked with the parity bit. If the parity bit matches the data, then the uart transmission is likely free of errors. 

### Stop bits
At the end of the data packet, the sending UART drives the TX line from low to high for 1 or 2 bits. 

| UART Summary | |
|:-----|---------:|
| Wires | 2 |
| Method of Transmission | Asynchronous |
| Serial or Parallel | Serial |
| Max number of Masters | 1 |
| Max number of Slaves | 1 |
| Speed | 4800, 9600, 19200, 38400, 57600, 115200, 230400, 460800, 921600 |


## References
- Eric Peňa and Mary Grace Legaspi. *UART: A Hardware Communication Protocol Understanding Universal Asynchronous Receiver/Transmitter* Analog Devices. Published on Dec 2020. Available at: [UART: A Hardware Communication Protocol Understanding Universal Asynchronous Receiver/Transmitter
](https://www.analog.com/en/resources/analog-dialogue/articles/uart-a-hardware-communication-protocol.html). Accessed on May 31, 2025.