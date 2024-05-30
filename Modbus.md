- model - Master-Slave (Client-Server over TCP/IP)
- Data: 
    1. RTU (Remote Terminal Unit) - binarne data
    2. ASCII
    3. TCP/IP
- Data model:
    1. Coil - 1b digital output (r/w)
    2. Discrete Input - 1b dig. input (r)
    3. Input register - 16b analog in (r)
    4. Holding register - 16b general purp. mem

```plantuml
participant Master
participant Slave

Master -> Slave : Request
Slave -> Slave : Action (eg. read/write memory)
Slave -> Master : Response
```
## Packet structure
### <mark style="background: #FFF3A3A6;">RTU packet</mark>
| Field | Bytes | Example Value | Description |
| ---- | ---- | ---- | ---- |
| Slave Address | 1 byte | 0x01 | Address of the target slave |
| Function Code | 1 byte | 0x03 | Function code for reading |
| Data | n bytes | 0x000A0002 | Starting address and quantity |
| CRC | 2 bytes | 0xC5DB | CRC value for error checking |
### <mark style="background: #FFF3A3A6;">ASCII packet</mark>
| Field | Characters | Example Value | Description |
| ---- | ---- | ---- | ---- |
| Start of Frame | 1 char | : | Start of frame character |
| Slave Address | 2 chars | 01 | Address of the target slave |
| Function Code | 2 chars | 03 | Function code for reading |
| Data | n chars | 000A0002 | Starting address and quantity |
| LRC | 2 chars | 1A | LRC value for error checking |
| End of Frame | 2 chars | CR LF | End of frame characters |
### <mark style="background: #ADCCFFA6;">TCP/IP packet</mark>
| Field | Bytes | Example Value | Description |
| ---- | ---- | ---- | ---- |
| Transaction Identifier | 2 bytes | 0x0001 | Transaction ID |
| Protocol Identifier | 2 bytes | 0x0000 | Protocol ID (0 for Modbus) |
| Length | 2 bytes | 0x0006 | Remaining bytes |
| Unit Identifier | 1 byte | 0x01 | Address of the target slave |
| Function Code | 1 byte | 0x03 | Function code for reading |
| Data | n bytes | 0x000A0002 | Starting address and quantity |

<mark style="background: #FFF3A3A6;">packet</mark> - Serial
<mark style="background: #ADCCFFA6;">packet</mark> - Ethernet