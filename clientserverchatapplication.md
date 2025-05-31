WE HAVE CREATED A CLIENT SERVER CHAT APPLICATION PROGRAM BY USING THE CONCEPT OF SOCKET PROGRAMMING USED IN JAVA..
CLIENT PROGRAM:-
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

            // Receive and display operation choices from the server
            String choices = input.readLine();
            System.out.println(choices);

            // Show operation choices
            System.out.println("Choose an operation:");
            System.out.println("1 - Check if numbers are odd or even");
            System.out.println("2 - Check if numbers are positive or negative");
            System.out.println("3 - Square of two numbers");
            System.out.println("4 - Disconnect client and server");
            System.out.print("Enter your choice: ");

            int choice = scanner.nextInt();
            output.println(choice);

            // Receive and display result from server
            String result = input.readLine();
            System.out.println("Server result: " + result);

            // Closing resources
            scanner.close();
            socket.close();

        } catch (IOException e) {
            System.err.println("Client Error: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
