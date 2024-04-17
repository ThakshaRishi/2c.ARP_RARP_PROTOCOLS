# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
1. Set up ARP requester and responder nodes with unique IP and MAC addresses.
2. Establish a TCP connection between requester and responder.
3. Request MAC address for a given IP from the requester.
4. Responder sends its MAC address in response.
5. Close TCP connection.
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP

Client:
```
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
c, addr = s.accept()

address = {"165.165.80.80": "6A:08:AA:C2", "165.165.79.1": "8A:BC:E3:FA"}

while True:
    ip = c.recv(1024).decode()
    try:
        mac = address[ip]
        c.send(mac.encode())
    except KeyError:
        c.send("Not Found".encode())

```

Server:
```
import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    ip = input("Enter logical Address: ")
    s.send(ip.encode())
    print("MAC Address:", s.recv(1024).decode())

```
## OUTPUT - ARP
![image](https://github.com/ThakshaRishi/2c.ARP_RARP_PROTOCOLS/assets/144870423/19e677a0-c093-4a06-ae70-46927b8e7940)

## PROGRAM - RARP
Client:
```
import socket
s = socket.socket()
s.bind(('localhost', 9000))
s.listen(5)
c, addr = s.accept()

address = {"6A:08:AA:C2": "192.168.1.100", "8A:BC:E3:FA": "192.168.1.99"}

while True:
    ip = c.recv(1024).decode()
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
```
Server:
```
import socket

s = socket.socket()
s.connect(('localhost', 9000))

while True:
    ip = input("Enter MAC Address: ")
    s.send(ip.encode())
    print("Logical Address:", s.recv(1024).decode())

```
## OUTPUT -RARP

![Screenshot 2024-04-17 105802](https://github.com/ThakshaRishi/2c.ARP_RARP_PROTOCOLS/assets/144870423/7c89c886-2849-4e01-ad66-b627489b57ad)

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
