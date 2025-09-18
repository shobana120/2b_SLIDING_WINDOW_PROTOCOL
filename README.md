# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL

## AIM
To implement the sliding window protocol.

## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
 
## PROGRAM
# Client.py
```
import socket

# Create a TCP socket
server_socket = socket.socket()
server_socket.bind(('localhost', 8000))
server_socket.listen(1)

print("Waiting for connection from server...")
connection, addr = server_socket.accept()
print(f"Connected to: {addr}")

# Take input from user
total_frames = int(input("Enter number of frames to send: "))
frames = list(range(total_frames))
window_size = int(input("Enter Window Size: "))

start = 0  # start index
while start < len(frames):
    end = start + window_size
    frame_batch = frames[start:end]  # take window-sized batch
    connection.send(str(frame_batch).encode())  # send batch
    ack = connection.recv(1024).decode()
    if ack:
        print(ack)
        start = end  # move sliding window

```
# Server.py

```
import socket

# Create TCP socket
client_socket = socket.socket()
client_socket.connect(('localhost', 8000))

while True:
    data = client_socket.recv(1024).decode()
    if not data:
        break
    print(data)
    client_socket.send("Acknowledgement received from the server".encode())
```

## OUPUT

# CLIENT

<img width="1920" height="1200" alt="Screenshot (135)" src="https://github.com/user-attachments/assets/b7d85777-e5cd-4fd2-87c5-749b0b9dfb20" />

# SERVER

<img width="1920" height="1200" alt="Screenshot (136)" src="https://github.com/user-attachments/assets/cba27f21-7fb7-4596-906d-c20cd1baef89" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
