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


##SERVER PROGRAM:-

package king;

import java.io.*;   //package for input output operations 
import java.net.*;  //package for doing socket connections

public class Server {
    public static void main(String[] args) {
        try (ServerSocket serverSocket = new ServerSocket(20074)) {
            System.out.println("Server is running and waiting for a client...");
            Socket socket = serverSocket.accept();
            System.out.println("Client connected!");
            
            BufferedReader input = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            PrintWriter output = new PrintWriter(socket.getOutputStream(), true);
            
            // Receive two numbers from the client
            int num1 = Integer.parseInt(input.readLine());
            int num2 = Integer.parseInt(input.readLine());
            
            // Send choices to the client
            output.println("Choose an operation:");
            
            int choice = Integer.parseInt(input.readLine());
            String result = "";
            
            
            switch (choice) {
                case 1:
                    result = "first number is: " + (num1 % 2 == 0 ? "Even" : "Odd") + ", second number is: " + (num2 % 2 == 0 ? "Even" : "Odd");
                    break;
                case 2:
                    result = "first number is: " + (num1 >= 0 ? "Positive" : "Negative") + ", second number is: " + (num2 >= 0 ? "Positive" : "Negative");
                    break;
                case 3:
                    result = "Square of first number: " + (num1 * num1) + ",square of second number is:" +(num2*num2);
                    break;
                case 4:
                	socket.close();
                	result="network disconnected";
                	break;
                	default:
                    result = "Invalid choice!!!!";
            }
            
            // Send result to client
            output.println(result);
            
            System.out.println("Result sent to client: " + result);
            
            // Connections will be automatically closed by try-with-resources
        } catch (IOException e) {
           System.out.println(e);
        }
    }
}
'''java
