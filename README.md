# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
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
```
import socket
c = socket.socket()
c.connect(('localhost', 9999))

size = int(input("Enter number of frames to send: "))
l = list(range(size))  
print("Total frames to send:", len(l))
s = int(input("Enter Window Size: "))

i = 0
while True:
    while i < len(l):
        st = i + s
        frames_to_send = l[i:st]  
        print(f"Sending frames: {frames_to_send}")
        c.send(str(frames_to_send).encode())  

        ack = c.recv(1024).decode()  
        if ack:
            print(f"Acknowledgment received: {ack}")
            i += s  

    break
c.close()
```
SERVER:
```
import socket
s = socket.socket()
s.bind(('localhost', 9999))
s.listen(1)
print("Server listening...")
conn, addr = s.accept()
print(f"Connected to {addr}")

while True:
    frames = conn.recv(1024).decode()
    if not frames:
        break

    print(f"Received frames: {frames}")
    ack_message = f"ACK for frames: {frames}"
    conn.send(ack_message.encode())

conn.close()  
s.close()
```
## OUPUT - ARP

![Screenshot (7)](https://github.com/user-attachments/assets/e0e362a2-fab5-4af0-8edb-e6a698d5f476)


![Screenshot (6)](https://github.com/user-attachments/assets/8cc137ae-bdd4-4a1c-b2b5-4096a0141eca)

## PROGRAM - RARP
CLIENT:
```
import socket
s=socket.socket()
s.bind(('localhost',9000))
s.listen(5)
c,addr=s.accept()
address={"6A:08:AA:C2":"192.168.1.100","8A:BC:E3:FA":"192.168.1.99"};
while True:
    ip=c.recv(1024).decode()
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
```
SERVER:
```
import socket
s=socket.socket()
s.connect(('localhost',9000))
while True:
    ip=input("Enter MAC Address : ")
    s.send(ip.encode())
    print("Logical Address",s.recv(1024).decode())
```
## OUPUT -RARP

![Screenshot 2025-04-26 140758](https://github.com/user-attachments/assets/06f0d436-bbe0-428c-8a0e-598c8e99bef2)

![Screenshot 2025-04-26 140733](https://github.com/user-attachments/assets/33fd051e-909f-4eaf-8f4d-cb2925e670fa)



## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
