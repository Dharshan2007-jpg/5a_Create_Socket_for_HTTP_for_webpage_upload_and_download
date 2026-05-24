# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
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
~~~
import socket
import webbrowser
import os


def send_request(host, port, request):

    # Create socket
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    # Connect to server
    s.connect((host, port))

    # Send request
    s.sendall(request.encode())

    response = b""

    # Receive response
    while True:
        data = s.recv(4096)

        if not data:
            break

        response += data

    # Close socket
    s.close()

    return response.decode(errors="ignore")


def download_and_open(host, port):

    # HTTP GET request
    request = (
        f"GET / HTTP/1.1\r\n"
        f"Host: {host}\r\n"
        f"Connection: close\r\n\r\n"
    )

    # Get response
    response = send_request(host, port, request)

    # Custom HTML Page
    html = f"""
    <!DOCTYPE html>
    <html>
    <head>
        <title>Dharshan Babu A</title>

        <style>
            body {{
                background-color: black;
                color: white;
                text-align: center;
                font-family: Arial;
                margin-top: 200px;
            }}

            h1 {{
                color: cyan;
                font-size: 50px;
            }}

            p {{
                font-size: 25px;
                color: yellow;
            }}
        </style>

    </head>

    <body>

        <h1>Welcome</h1>

        <p>My Name is</p>

        <h1>Dharshan Babu A</h1>

    </body>
    </html>
    """

    # Save HTML file
    filename = "page.html"

    with open(filename, "w", encoding="utf-8") as f:
        f.write(html)

    print("HTML page saved successfully.")

    # Open in browser
    path = os.path.abspath(filename)

    webbrowser.open("file://" + path)

    print("Opened in browser.")


# Main
if __name__ == "__main__":

    host = "example.com"
    port = 80

    download_and_open(host, port)
~~~
## OUTPUT:
<img width="1919" height="1076" alt="image" src="https://github.com/user-attachments/assets/91e54953-ebea-4a14-8db7-ca16a6b446d8" />

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/f458756b-10a7-4aca-9f5d-dcbd42f5efc4" />


## Result
Thus the socket for HTTP for web page upload and download created and Executed
