Got it 👍 — you want the program to take dynamic input (not a hardcoded "hello_client" string).

Here’s a short, runnable, dynamic Java version of a simple TCP client-server setup:

The server listens for a single connection and prints what it receives.

The client takes user input dynamically and sends it to the server.



---

🖥️ Server.java

import java.net.*;
import java.io.*;

public class Server {
    public static void main(String[] args) throws IOException {
        ServerSocket ss = new ServerSocket(5000);
        System.out.println("Server listening on port 5000...");
        Socket s = ss.accept();
        System.out.println("Client connected.");
        BufferedReader in = new BufferedReader(new InputStreamReader(s.getInputStream()));
        String msg;
        while ((msg = in.readLine()) != null)
            System.out.println("Received: " + msg);
        s.close();
        ss.close();
    }
}


---

💻 Client.java

import java.net.*;
import java.io.*;

public class Client {
    public static void main(String[] args) throws IOException {
        Socket s = new Socket("127.0.0.1", 5000);
        PrintWriter out = new PrintWriter(s.getOutputStream(), true);
        BufferedReader userIn = new BufferedReader(new InputStreamReader(System.in));

        System.out.print("Enter message: ");
        String message = userIn.readLine();
        out.println(message);

        s.close();
    }
}


---

▶️ How to Run

1. Save both files in the same folder.


2. Compile:

javac Server.java Client.java


3. Run the server first:

java Server


4. Then run the client:

java Client


5. When prompted, type your message (e.g. hello_client), hit Enter, and the server will print it:

Server listening on port 5000...
Client connected.
Received: hello_client




---

Would you like me to make it bi-directional next (so the server can also send responses back)?
