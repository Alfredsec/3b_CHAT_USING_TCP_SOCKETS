# 3b.CREATION FOR CHAT USING TCP SOCKETS
## AIM
To write a python program for creating Chat using TCP Sockets Links.
## ALGORITHM:
1. Import the necessary modules in python
2. Create a socket connection to using the socket module.
3. Send message to the client and receive the message from the client using the Socket module in
 server
4. Send and receive the message using the send function in socket.
## PROGRAM
### SERVER
```
import socket
import threading

def handle_client(client_socket):
    while True:
        try:
            # Receive message from client
            message = client_socket.recv(1024).decode()
            if not message:
                break
            print(f"Received message: {message}")

            # Send message back to client
            client_socket.sendall(message.encode())
        except:
            break

    client_socket.close()

def start_server():
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server_socket.bind(('127.0.0.1', 5555))
    server_socket.listen(5)
    print("Server started, listening on port 5555")

    while True:
        client_socket, addr = server_socket.accept()
        print(f"Accepted connection from {addr}")
        client_handler = threading.Thread(target=handle_client, args=(client_socket,))
        client_handler.start()

start_server()
```
### CILENT
```
import socket

def start_client():
    client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    client_socket.connect(('127.0.0.1', 5555))

    while True:
        message = input("Enter message to send to server (or type 'exit' to quit): ")
        if message.lower() == 'exit':
            break
        client_socket.sendall(message.encode())

        # Receive response from server
        response = client_socket.recv(1024).decode()
        print(f"Received from server: {response}")

    client_socket.close()

start_client()
```

## OUPUT
### SERVER 
![310515466-6ec0c504-a719-4feb-bf69-bec451a22fb9](https://github.com/Alfredsec/3b_CHAT_USING_TCP_SOCKETS/assets/120621608/f650bc0b-19aa-4033-931e-f081eb740128)


### CILENT
![310515522-0b33d00d-a03b-4ca7-add7-4e6650d0301a](https://github.com/Alfredsec/3b_CHAT_USING_TCP_SOCKETS/assets/120621608/4a0a51bb-4ec6-4eb1-ab09-74eafd8708d8)


## RESULT
Thus, the python program for creating Chat using TCP Sockets Links was successfully 
created and executed.
