# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## NAME: PRAGATHI KUMAR
## REGISTER NUMBER : 212224230200
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>
## Program

```
import socket

host = 'localhost'
port = 8000 # Use a common web port like 8080

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.bind((host, port))
s.listen(5)

print(f"Server running at http://{host}:{port}/")

while True:
    conn, addr = s.accept()
    print("Connected by", addr)
    request = conn.recv(1024).decode()
    print("Request received:\n", request)

    try:
        with open("index.html", "rb") as f:
            response_body = f.read()
        response_header = (
            "HTTP/1.1 200 OK\r\n"
            "Content-Type: text/html\r\n"
            f"Content-Length: {len(response_body)}\r\n"
            "Connection: close\r\n"
            "\r\n"
        ).encode()
        conn.sendall(response_header + response_body)
    except FileNotFoundError:
        response = "HTTP/1.1 404 Not Found\r\n\r\nFile not found".encode()
        conn.sendall(response)

    conn.close()

```

index.html

```
<!DOCTYPE html>
<html>
<head>
    <title>Python Socket Server</title>
</head>
<body>
    <h1>Hello from Python socket server</h1>
    <p>This page is served by your Python socket server!</p>
</body>
</html>

```


## OUTPUT
<img width="1518" height="1126" alt="image" src="https://github.com/user-attachments/assets/b59a186f-5312-4336-a4c8-166aa116ceb9" />
<img width="1245" height="1148" alt="image" src="https://github.com/user-attachments/assets/0be3e8df-d566-4e7e-94a8-df617e806b90" />



## Result
Thus the socket for HTTP for web page upload and download created and Executed
