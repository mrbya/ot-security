- used in HVAC
#### Features

- **Interoperability**: Enables devices from different manufacturers to communicate and work together within a building automation system.
- **Standardized Objects and Services**: Defines a set of standard objects (like Analog Input, Binary Output) and services (like Read Property, Write Property) to ensure consistent behavior.
- **Scalability**: Suitable for small to large-scale building automation systems.
- **Multiple Networking Options**: Supports various physical and link layers, including Ethernet, ARCNET, MS/TP (RS-485), and LonTalk.
### Packet Structure

BACnet protocol data units (PDUs) are used for communication between devices. The structure of a BACnet packet can vary depending on the network layer used, but here we'll outline the common structure found in BACnet over IP (BACnet/IP), one of the most commonly used transport methods.

**BACnet/IP Frame Structure:**

1. **Ethernet Header**:
    
    - **Destination MAC Address**: 6 bytes
    - **Source MAC Address**: 6 bytes
    - **Type**: 2 bytes (typically `0x0800` for IPv4)
2. **IP Header**:
    
    - **Version and Header Length**: 1 byte
    - **Differentiated Services Field**: 1 byte
    - **Total Length**: 2 bytes
    - **Identification**: 2 bytes
    - **Flags and Fragment Offset**: 2 bytes
    - **Time to Live (TTL)**: 1 byte
    - **Protocol**: 1 byte (typically `0x11` for UDP)
    - **Header Checksum**: 2 bytes
    - **Source IP Address**: 4 bytes
    - **Destination IP Address**: 4 bytes
3. **UDP Header**:
    
    - **Source Port**: 2 bytes
    - **Destination Port**: 2 bytes
    - **Length**: 2 bytes
    - **Checksum**: 2 bytes
4. **BACnet/IP Header**:
    
    - **BVLC Type**: 1 byte (BACnet Virtual Link Control Type, typically `0x81`)
    - **BVLC Function**: 1 byte (function code, e.g., `0x0A` for Original-Unicast-NPDU)
    - **BVLC Length**: 2 bytes (length of the BVLC message including header)
5. **BACnet NPDU (Network Protocol Data Unit)**:
    
    - **Protocol Version**: 1 byte (`0x01` for BACnet)
    - **NPDU Control**: 1 byte (flags indicating network layer message, destination specifier, etc.)
    - **Destination Network Address**: 2 bytes (optional, used if the destination is specified)
    - **Destination MAC Address**: Variable length (optional)
    - **Source Network Address**: 2 bytes (optional)
    - **Source MAC Address**: Variable length (optional)
    - **Hop Count**: 1 byte (optional)
    - **Network Layer Message Type**: 1 byte (if NPDU Control indicates a network layer message)
6. **BACnet APDU (Application Protocol Data Unit)**:
    
    - **APDU Type**: 1 byte (indicates the type of APDU, such as Confirmed Request, Unconfirmed Request, Simple ACK, Complex ACK, etc.)
    - **Service Choice**: 1 byte (indicates the type of service, such as Read Property, Write Property, etc.)
    - **Invoke ID**: 1 byte (identifier for matching requests and responses)
    - **Service Parameters**: Variable length (parameters for the service request or response)

### Example BACnet/IP Packet

A typical BACnet/IP packet for a Read Property service request might look like this:

- **Ethernet Header**: Contains destination and source MAC addresses, and type field.
- **IP Header**: Contains source and destination IP addresses, and other IP layer information.
- **UDP Header**: Contains source and destination ports, and UDP-specific information.
- **BACnet/IP Header**: Contains BVLC Type, BVLC Function, and BVLC Length.
- **BACnet NPDU**: Contains protocol version, NPDU control flags, and optional addressing fields.
- **BACnet APDU**: Contains APDU type, service choice, invoke ID, and service parameters such as object identifier and property identifier.

### Example Use Cases

- **HVAC Systems**: Controls heating, ventilation, and air conditioning systems in buildings.
- **Lighting Control**: Manages lighting systems for energy efficiency and user comfort.
- **Access Control**: Integrates with security systems to control building access.
- **Fire Detection and Alarm Systems**: Interfaces with fire safety systems for monitoring and control.