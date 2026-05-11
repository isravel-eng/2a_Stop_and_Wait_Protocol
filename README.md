# 2a_Stop_and_Wait_Protocol

## AIM
To write a python program to perform Stop and Wait Protocol.

## ALGORITHM
1. Start the program.
2. Create a socket connection between sender and receiver.
3. Get the number of frames from the user.
4. Sender sends frames to the receiver.
5. Receiver receives frames and sends ACK.
6. Sender waits for ACK before sending the next frame.
7. Stop the program.

## PROGRAM

### sender.py
```python
import socket

s = socket.socket()
s.connect(('localhost', 8000))

n = int(input("Enter number of frames: "))

for i in range(n):
    msg = input("Enter frame: ")
    s.send(msg.encode())

    ack = s.recv(1024).decode()
    print("Received:", ack)

s.close()
```

### receiver.py
```python
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)

print("Waiting for connection...")
conn, addr = s.accept()
print("Connected to", addr)

while True:
    data = conn.recv(1024).decode()
    if not data:
        break

    print("Frame received:", data)
    conn.send("ACK".encode())

conn.close()
```

## OUTPUT

### Receiver Side
```text
Waiting for connection...
Connected to ('127.0.0.1', 52618)
Frame received: Hello
Frame received: Frame1
Frame received: Frame2
```
<img width="647" height="136" alt="image" src="https://github.com/user-attachments/assets/374574a5-0fc3-4777-a764-466cf47f2344" />


### Sender Side
```text
Enter number of frames: 3
Enter frame: Hello
Received: ACK
Enter frame: Frame1
Received: ACK
Enter frame: Frame2
Received: ACK
```
<img width="639" height="181" alt="image" src="https://github.com/user-attachments/assets/3a5e44d6-6cf9-4644-80cb-f1088e061101" />


## RESULT
Thus, the python program to perform Stop and Wait Protocol was successfully executed.
