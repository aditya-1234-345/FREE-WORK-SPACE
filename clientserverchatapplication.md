WE HAVE CREATED A CLIENT SERVER CHAT APPLICATION PROGRAM BY USING THE CONCEPT OF SOCKET PROGRAMMING USED IN JAVA..
CLIENT PROGRAM:-
'''package king;

import java.io.*;
import java.net.*;
import java.util.Scanner;

public class Client {
    public static void main(String[] args) {
        try (Socket socket = new Socket("localhost", 20074)) {
            System.out.println("Connected to server!");
            
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
            System.out.print("Enter your choice: enter 1 for odd and even check ,"
            		+ " \n 2 for positive and negative and "
            		+ "\n 3  or square of two numbers "
            		+ "\n  enter 4 for disconnection of client and server ");
            int choice = scanner.nextInt();
            output.println(choice);
            
            
            // Receive and display result
            String result = input.readLine();
            System.out.println("server result: " + result);
            socket.close();
            scanner.close();
            // Connections will be automatically closed by try-with-resources
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}'''
