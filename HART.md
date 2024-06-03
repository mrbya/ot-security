- digital communication over the existing 4-20 mA 
- widely used in process industries for communication between smart field devices and control systems

#### Features

- **Hybrid Communication**: Combines digital communication with the 4-20 mA analog signal.
- **Device Interoperability**: Allows devices from different manufacturers to communicate.
- **Two-Way Communication**: Enables both sending and receiving data.
- **Diagnostics and Configuration**: Supports device diagnostics and configuration without interrupting the analog signal.

### HART Packet Structure

- master-slave protocol

**HART Frame Structure:**

1. **Preamble**: Typically 5-20 bytes of `0xFF` used for synchronization.
2. **Start Delimiter**: 1 byte (`0x02` for primary master, `0x82` for secondary master).
3. **Address**: 1 byte (4 bits for short frame, 20 bits for long frame).
4. **Command**: 1 byte indicating the command type.
5. **Data Length**: 1 byte specifying the number of data bytes.
6. **Data**: Variable length, contains the actual data.
7. **Checksum**: 1 byte, used for error checking.

### HART-IP

HART-IP extends the HART protocol to IP networks, allowing HART devices to communicate over Ethernet or Wi-Fi networks. This enables integration with modern networked control systems and facilitates remote monitoring and configuration.

#### Features

- **IP Network Compatibility**: Uses standard IP networks for communication.
- **Integration**: Seamlessly integrates with existing HART devices.
- **Remote Access**: Facilitates remote device monitoring and configuration.

### HART-IP Packet Structure

HART-IP encapsulates traditional HART messages within IP packets.

**HART-IP Frame Structure:**

1. **Ethernet Header**: Standard Ethernet frame header.
2. **IP Header**: Standard IP header for routing.
3. **TCP/UDP Header**: Transport layer header (typically UDP for HART-IP).
4. **HART-IP Header**:
    - **Message Type**: Specifies the type of HART message.
    - **Sequence Number**: For tracking message order.
5. **HART Message**: Encapsulated traditional HART message.
6. **Checksum**: For error checking.

### WirelessHART

- wireless extension of HART

#### Features

- **Mesh Networking**: Devices form a self-healing and self-organizing network.
- **Security**: Uses AES-128 encryption for secure communication.
- **Reliability**: Redundant paths ensure reliable data transmission.
- **Flexibility**: Supports easy installation and scalability.

### WirelessHART Packet Structure

- uses IEEE 802.15.4 standard for the physical layer and MAC layer communication

**WirelessHART Frame Structure:**

1. **Preamble**: Used for synchronization.
2. **Start of Frame Delimiter (SFD)**: Indicates the start of the frame.
3. **Frame Control**: Specifies frame type and addressing mode.
4. **Sequence Number**: For tracking frame order.
5. **Addressing Information**: Source and destination addresses.
6. **Network Layer**:
    - **Network ID**: Identifies the WirelessHART network.
    - **Message Type**: Specifies the type of WirelessHART message.
    - **Command**: Indicates the command type.
    - **Data**: Contains the payload data.
7. **MAC Layer**:
    - **MAC Payload**: Encapsulates the network layer message.
8. **Checksum**: For error detection and correction.

### Example use cases

- **HART**: Used for communication in process industries where 4-20 mA instrumentation is prevalent, such as in chemical plants and refineries.
- **HART-IP**: Employed in modern control systems requiring integration with IP networks, enabling remote monitoring and control.
- **WirelessHART**: Ideal for applications requiring wireless communication, such as in difficult-to-wire locations or where mobility is needed, like in large industrial complexes.