Sure, Jesy 😊 — here’s a complete write-up for your UDP Echo Client–Server Java program, including Aim, Procedure, Program, Output, and Result — written in a clear and neat format (ideal for lab records or reports).


---

🧠 Aim

To develop a Java program to implement a UDP Echo Client and Server where the server echoes back the message received from the client.


---

⚙️ Procedure

1. Start the server:

Create a DatagramSocket bound to a specific port (e.g., 12345).

Wait for a packet from a client using socket.receive().

Display the received message.

Send the same data back to the client (echo).



2. Run the client:

Create a DatagramSocket (no need to bind a port manually).

Convert the message into bytes and send it to the server using DatagramPacket.

Wait for the echoed message from the server.

Display the received echoed message.



3. Verify the echo:

Check if the received message matches the one sent.





---

💻 Program

EchoServer.java
```
import java.net.*;

public class EchoServer {
    public static void main(String[] args) throws Exception {
        DatagramSocket socket = new DatagramSocket(12345);
        System.out.println("Server started... Waiting for messages...");

        byte[] buffer = new byte[1024];

        while (true) {
            DatagramPacket packet = new DatagramPacket(buffer, buffer.length);
            socket.receive(packet);

            String received = new String(packet.getData(), 0, packet.getLength());
            System.out.println("Received from client: " + received);

            // Echo back the received message
            DatagramPacket echo = new DatagramPacket(packet.getData(), packet.getLength(),
                                                     packet.getAddress(), packet.getPort());
            socket.send(echo);
        }
    }
}

```
---

EchoClient.java

```
import java.net.*;

public class EchoClient {
    public static void main(String[] args) throws Exception {
        DatagramSocket socket = new DatagramSocket();
        InetAddress server = InetAddress.getByName("localhost");
        int port = 12345;

        String message = "Hello Server!";
        byte[] data = message.getBytes();

        // Send message to server
        socket.send(new DatagramPacket(data, data.length, server, port));

        // Receive echo from server
        byte[] buffer = new byte[1024];
        DatagramPacket response = new DatagramPacket(buffer, buffer.length);
        socket.receive(response);

        String echoed = new String(response.getData(), 0, response.getLength());
        System.out.println("Sent: " + message);
        System.out.println("Received: " + echoed);

        socket.close();
    }
}

```
---

🧩 Sample Output

Server Output:

Server started... Waiting for messages...
Received from client: Hello Server!

Client Output:

Sent: Hello Server!
Received: Hello Server!


---

✅ Result

Thus, the Java program for the UDP Echo Client and Server was successfully executed.
The server received a message from the client and sent back the same message, verifying successful UDP communication.


---

Would you like me to make this version interactive (so the client can send multiple messages until typing “exit”)? That would be a good “extended” version for your record.
