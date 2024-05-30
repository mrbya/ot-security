- model - Publish-Subscribe (broker brokers messages based on subscribed clients)
- relies on TCP/IP

![[MQTT.png]]
### Packet structure
#### Fixed Header

The fixed header is present in all MQTT control packets and consists of two fields:

1. **Control Packet Type** (4 bits): Specifies the type of MQTT packet (e.g., CONNECT, PUBLISH).
2. **Flags** (4 bits): Specific to each packet type.
3. **Remaining Length**: Encodes the number of bytes remaining within the current packet, including variable header and payload.

#### Variable Header:

The variable header is present in some MQTT control packets and its content depends on the packet type.

- **CONNECT Packet**: Contains protocol name, version, connection flags, keep-alive timer, etc.
- **PUBLISH Packet**: Contains the topic name and packet identifier (for QoS 1 and QoS 2).

#### Payload:

The payload is also specific to the packet type.

- **CONNECT Packet**: Contains the client identifier, will topic, will message, username, and password.
- **PUBLISH Packet**: Contains the application message to be delivered to the subscribers.

**Example CONNECT Packet Structure:**

1. **Fixed Header**:
    
    - Control Packet Type: 1 (CONNECT)
    - Flags: 0
    - Remaining Length: Variable
2. **Variable Header**:
    
    - Protocol Name: `MQTT`
    - Protocol Level: 4 (MQTT 3.1.1)
    - Connect Flags: Various flags for username, password, will, etc.
    - Keep Alive: Time interval in seconds
3. **Payload**:
    
    - Client Identifier: Unique ID for the client
    - Will Topic: Optional
    - Will Message: Optional
    - Username: Optional
    - Password: Optional

**Example PUBLISH Packet Structure:**

1. **Fixed Header**:
    
    - Control Packet Type: 3 (PUBLISH)
    - Flags: QoS level, retain flag, duplicate delivery flag
    - Remaining Length: Variable
2. **Variable Header**:
    
    - Topic Name: The topic to which the message is published
    - Packet Identifier: Present if QoS is 1 or 2
3. **Payload**:
    
    - The actual message content being published

### MQTT Control Packet Types:

- **CONNECT (1)**: Client request to connect to the broker.
- **CONNACK (2)**: Connect acknowledgment.
- **PUBLISH (3)**: Publish message.
- **PUBACK (4)**: Publish acknowledgment for QoS 1.
- **PUBREC (5)**: Publish received (part of QoS 2).
- **PUBREL (6)**: Publish release (part of QoS 2).
- **PUBCOMP (7)**: Publish complete (part of QoS 2).
- **SUBSCRIBE (8)**: Client subscribe request.
- **SUBACK (9)**: Subscribe acknowledgment.
- **UNSUBSCRIBE (10)**: Client unsubscribe request.
- **UNSUBACK (11)**: Unsubscribe acknowledgment.
- **PINGREQ (12)**: PING request.
- **PINGRESP (13)**: PING response.
- **DISCONNECT (14)**: Client disconnect notification.

### Applications

- Internet of Things (IoT)
- Mobile Messaging
- Remote Monitoring