# CLIENT SERVER CHAT APPLICATION
We have created a client-server chat application program using the concept of **socket programming** in Java.
---

## CLIENT PROGRAM

```java
package king;

import java.io.*;
import java.net.*;
import java.util.Scanner;

/**
 * A simple client that connects to a server on localhost at port 20074.
 * It sends two numbers, allows the user to choose an operation, and receives the result from the server.
 */
public class Client {
    public static void main(String[] args) {
        try (Socket socket = new Socket("localhost", 20074)) {
            System.out.println("Connected to server!");

            // Setup input/output streams
            BufferedReader input = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            PrintWriter output = new PrintWriter(socket.getOutputStream(), true);
            Scanner scanner = new Scanner(System.in);

            // Enter two numbers
            System.out.print("Enter first number: ");
            int num1 = scanner.nextInt();
            System.out.print("Enter second number: ");
            int num2 = scanner.nextInt();

            // Send numbers to the server
            output.println(num1);
            output.println(num2);

            // Receive and display choices
            String choices = input.readLine();
            System.out.println(choices);

            // Choose an operation
            System.out.println("Enter your choice:");
            System.out.println("1 - Check Odd/Even");
            System.out.println("2 - Check Positive/Negative");
            System.out.println("3 - Square of numbers");
            System.out.println("4 - Disconnect");
            System.out.print("Your choice: ");
            int choice = scanner.nextInt();
            output.println(choice);

            // Receive and display result
            String result = input.readLine();
            System.out.println("Server result: " + result);

            scanner.close();
            socket.close();

        } catch (IOException e) {
            System.err.println("Client Error: " + e.getMessage());
            e.printStackTrace();
        }
    }
}

