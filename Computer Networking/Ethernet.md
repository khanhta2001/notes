1. CSMA/ CD (Carrier Sense Multiple Access with Collision Detection)
   Carrier Sense: before a device transmits data, it senses or listens to the network to determine whether another device is transmitting. If the network is busy, it will wait before sending data.
   Multiple Access: Multiple devices can connect to and access the network. They all follow the same rules about sensing for carrier signals before transmission to avoid simultaneous data sending.
   Collision Detection: despite the precautions, sometimes collisions happen - this is when two devices transmit data at the same time. When a collision occurs, it creates a unique signal pattern on the network. All the devices that are transmitting will recognize this pattern, understand a collision has occurred, and stop transmitting immediately. 
   After a collision, device use backoff algorithm to randomize the time they need to wait before attempting to transmit again. This process helps to minimize further collisions. In ethernet networks, after 16 consecutive collisions, the node gives up and attempts retransmission later. 
   
2. Frame structure
   1. Preamble: It is used to tell receiving systems that a frame is starting and to synchronize the clocks.
   2. Start of frame: it is another signal to indicate the beginning of the frame.
   3. Destination Address: this field holds the address of the device to which the frame is being sent. Every device on a network has unique address. 
   4. Source address: this field holds the address of the device that sent the frame
   5. Type/Length: this field indicates whether what follows is the ethernet type or the payload
   6. Payload/data: this field holds the actual data being transported. It can vary in size. On an ethernet network, it typically ranges from 46-15000 bytes. 
   7. Pad: if a data field is less than minimum size, this field fills with extra byte to bring the data field up to the minimum length
   8. Error Checking/ CRC: the frame ends with an error checking field commonly a cyclic redundancy check. it allows the receiving device to check if the frame arrived correctly.
      
3. Ethernet
   1. Network architecture: ethernet provides a simple and effective technology that connects devices in close proximity, like within a building or a home. The architecture involves running an ethernet cable from each device to a central switch or hub.
   2. Data Transfer Method: Ethernet uses the CSMA/CD protocol for data transmission. It means that many hosts can access the network through the same cable, listening for carrier signals before transmitting. If a collision occurs, the protocol detects and retransmits the data.
   3. Speed and performance: ethernet speed have improved dramatically from 10mbps to 10 gpbs and beyond. 
   4. Frame structure: Ethernet data is broken into frames, each containing source and destination addresses, error-checking information, and the payload data. 
4. MAC addresses
   A MAC address is a unique identifier assigned to network interfaces for communications on the physical network segment. It is hardwired or assigned for communications on the physical network segment. 
   
   A MAC address consists of six sets of two alphanumeric characters, separated by colons, hyphens, or without any separators. Each MAC address is unique to the device it is assigned to, and this provides a reliable way for networks to track and connect to specific devices.
   
5. Collision Detection: Exponential Backoff Algorithm
   1. if detected devices will stop transmitting.
   2. Each devices will wait a random amount of time before attempting to transmit again, the randomness helps to prevent the devices from transmitting simultaneously and causing another collision.
   3. For the first collision, the device will wait either 0 or 1 slot of time. Here a slot of time is a unit of time related to how long it takes for a network signal to travel across the network
   4. If another collision happens on the next try, the device double the maximum length of waiting time, 1,2,3,4,5 slot times.
   5. This process continues with the waiting time doubling for each successive collision, up to a specified maximum
   6. Once the message gets through without collision, the device resets its backoff algorithm and returns to the minimum slot time when new transmission happens. 
   7. Helps manage network traffic, reduces chances of collisions, and improves network performance. 
      
6. Ethernet Learning Algorithm
   Bridge learning Algorithm, used by network switches to learn and keep a table of AMC addresses. each switch maintains a table known as Forwarding Information Base, which maps each MAC address to the corresponding physical port. When a frame arrives at a switch, the switch checks the source AMC address and updates its FIB to indicate that the source device can be reached through the port where the frame entered. If a message arrives with a destination MAC address not in the switch's FIB, it floods the message out of all its port except the one it arrived on. Through this iterative learning process. The switch builds a complete table of devices and associated ports.
   
7. MAC Flooding
   This is a type of network attack where a switch is flooded with packets, each containing different source of MAC addresses. The intention is to consume the limit of switch's ability to store source MAC addresses. After its MAC table is full, the switch enters a state fail-open mode, when it acts as a hub and broadcast incoming packets to all ports. In this state, an attacker can receive traffic not intended for them and gather information on the network. 
   
8. Distributed Spanning Tree Algorithm 
   
   the Spanning Tree Protocol is used to create a loop free topology in a network with redundant paths. In a network of interconnected switches, redundant paths could cause loops where frames circle indefinitely. STP uses the spanning tree algorithm to select a root switch first and then calculate the shortest path to the root switch from every other switch. Every switch communicates with others through Bridge Protocol Data units to establish the best path. Redundant paths are then blocked out (but kept as backups in case of a primary path failure). Different instances of STP running on different Virtual LANs independently are regarded as a distributed spanning tree. Root is picked randomly using its unique identifier. If the distance are the same, pick randomly through assigning each a number and the lowest number gets picked. 