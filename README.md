# 2a_Stop_and_Wait_Protocol

## AIM
To write a python program to perform Stop and Wait Protocol.

## ALGORITHM
1. Start the program.
2. Create a socket connection between sender and receiver.
3. Get the number of frames from the user.
4. Send frames from receiver side to sender side.
5. Sender receives each frame and sends ACK.
6. Receiver waits for ACK before sending the next frame.
7. Stop the program.

## PROGRAM

### sender.py
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

### receiver.py
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

## OUTPUT

### Sender Side
```text
Waiting for connection...
Connected to ('127.0.0.1', 52618)
Frame received: Hello
Frame received: Frame1
Frame received: Frame2
```

### Receiver Side
```text
Enter number of frames: 3
Enter frame: Hello
Received: ACK
Enter frame: Frame1
Received: ACK
Enter frame: Frame2
Received: ACK
```

## RESULT
Thus, the python program to perform Stop and Wait Protocol was successfully executed.
