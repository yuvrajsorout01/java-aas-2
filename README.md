# java-aas-2
/**
 * The Calculator class provides methods to perform basic arithmetic operations.
 * It demonstrates method overloading for the addition operation and includes
 * handling for specific cases like division by zero.
 */
public class Calculator {

    /**
     * Adds two integers.
     * @param a The first integer.
     * @param b The second integer.
     * @return The sum of the two integers.
     */
    public int add(int a, int b) {
        return a + b;
    }

    /**
     * Adds two double-precision floating-point numbers.
     * This is an overloaded version of the add method.
     * @param a The first double.
     * @param b The second double.
     * @return The sum of the two doubles.
     */
    public double add(double a, double b) {
        return a + b;
    }

    /**
     * Adds three integers.
     * This is another overloaded version of the add method.
     * @param a The first integer.
     * @param b The second integer.
     * @param c The third integer.
     * @return The sum of the three integers.
     */
    public int add(int a, int b, int c) {
        return a + b + c;
    }

    /**
     * Subtracts the second integer from the first.
     * @param a The minuend.
     * @param b The subtrahend.
     * @return The difference between the two integers.
     */
    public int subtract(int a, int b) {
        return a - b;
    }

    /**
     * Multiplies two double-precision floating-point numbers.
     * @param a The first double.
     * @param b The second double.
     * @return The product of the two doubles.
     */
    public double multiply(double a, double b) {
        return a * b;
    }

    /**
     * Divides the first integer by the second.
     * Throws an IllegalArgumentException if the divisor is zero.
     * @param a The dividend.
     * @param b The divisor.
     * @return The result of the division as a double.
     * @throws IllegalArgumentException if b is 0.
     */
    public double divide(int a, int b) {
        if (b == 0) {
            // As required, handle the divide-by-zero error.
            throw new IllegalArgumentException("Error: Division by zero is not allowed.");
        }
        // Cast 'a' to double to ensure floating-point division.
        return (double) a / b;
    }
}
import java.util.InputMismatchException;
import java.util.Scanner;

/**
 * The UserInterface class provides a menu-driven console interface
 * for the Calculator application. It handles user input and interacts
 * with the Calculator class to perform operations.
 */
public class UserInterface {

    // Scanner object for input, as specified.
    private static final Scanner scanner = new Scanner(System.in);
    private static final Calculator calculator = new Calculator();

    /**
     * The main method to start the calculator application.
     * @param args Command line arguments (not used).
     */
    public static void main(String[] args) {
        mainMenu();
        scanner.close();
    }

    /**
     * Displays the main menu and handles user choices for navigation.
     */
    public static void mainMenu() {
        boolean exit = false;
        while (!exit) {
            System.out.println("\nWelcome to the Calculator Application!");
            System.out.println("1. Add Numbers");
            System.out.println("2. Subtract Numbers");
            System.out.println("3. Multiply Numbers");
            System.out.println("4. Divide Numbers");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");

            try {
                int choice = scanner.nextInt();
                switch (choice) {
                    case 1:
                        performAddition();
                        break;
                    case 2:
                        performSubtraction();
                        break;
                    case 3:
                        performMultiplication();
                        break;
                    case 4:
                        performDivision();
                        break;
                    case 5:
                        exit = true;
                        System.out.println("Thank you for using the calculator!");
                        break;
                    default:
                        System.out.println("Invalid choice. Please enter a number between 1 and 5.");
                }
            } catch (InputMismatchException e) {
                System.out.println("Invalid input. Please enter a number.");
                scanner.next(); // Clear the invalid input from the scanner
            }
        }
    }

    /**
     * Handles the logic for addition, allowing the user to choose
     * between the overloaded add methods.
     */
    public static void performAddition() {
        System.out.print("Add (2) or (3) numbers? ");
        try {
            int count = scanner.nextInt();
            if (count == 2) {
                System.out.print("Enter first number (integer): ");
                int a = scanner.nextInt();
                System.out.print("Enter second number (integer): ");
                int b = scanner.nextInt();
                System.out.println("Result: " + calculator.add(a, b));
            } else if (count == 3) {
                System.out.print("Enter first number (integer): ");
                int a = scanner.nextInt();
                System.out.print("Enter second number (integer): ");
                int b = scanner.nextInt();
                System.out.print("Enter third number (integer): ");
                int c = scanner.nextInt();
                System.out.println("Result: " + calculator.add(a, b, c));
            } else {
                 System.out.println("Invalid choice. You can add 2 or 3 numbers.");
            }
             // Note: The prompt also specified an add(double, double) method.
             // This can be added as another sub-menu if needed, for instance,
             // by asking the user for the data type (integer or double).
        } catch (InputMismatchException e) {
            System.out.println("Invalid input. Please enter integers only.");
            scanner.next(); // Clear the buffer
        }
    }

    /**
     * Prompts for two integers and performs subtraction.
     */
    public static void performSubtraction() {
        try {
            System.out.print("Enter first number (integer): ");
            int a = scanner.nextInt();
            System.out.print("Enter second number (integer): ");
            int b = scanner.nextInt();
            System.out.println("Result: " + calculator.subtract(a, b));
        } catch (InputMismatchException e) {
            System.out.println("Invalid input. Please enter integers only.");
            scanner.next(); // Clear the buffer
        }
    }

    /**
     * Prompts for two doubles and performs multiplication.
     */
    public static void performMultiplication() {
        try {
            System.out.print("Enter first number (double): ");
            double a = scanner.nextDouble();
            System.out.print("Enter second number (double): ");
            double b = scanner.nextDouble();
            System.out.println("Result: " + calculator.multiply(a, b));
        } catch (InputMismatchException e) {
            System.out.println("Invalid input. Please enter numbers only.");
            scanner.next(); // Clear the buffer
        }
    }

    /**
     * Prompts for two integers and performs division,
     * handling the divide-by-zero error gracefully.
     */
    public static void performDivision() {
        try {
            System.out.print("Enter the dividend (integer): ");
            int a = scanner.nextInt();
            System.out.print("Enter the divisor (integer): ");
            int b = scanner.nextInt();
            double result = calculator.divide(a, b);
            System.out.println("Result: " + result);
        } catch (InputMismatchException e) {
            System.out.println("Invalid input. Please enter integers only.");
            scanner.next(); // Clear the buffer
        } catch (IllegalArgumentException e) {
            // Catches the specific exception thrown by the divide method
            System.out.println(e.getMessage());
        }
    }
}
