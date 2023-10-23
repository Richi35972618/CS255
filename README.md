# CS255

Journal


My attempt for our client DriverPass was not my best work. I failed to take into account all the details before starting. Their system was meant to be only the "On the Road" appointments and the details that that would entail. Knowing what I know now I would have built a strong scheduling system to keep the cars running on time and lessen the headaches of possible double bookings. The users needs are the job, if a user is not pleased with the work then the working is not done. My key learning point from this is to look over every detail and every piece of intel before going into the project. This is something I will learn from and not repeat.


public class AccountNumberGenerator {

    private static AccountNumberGenerator instance;
    private int nextAccountNumber = 1;

    // Private constructor to prevent direct instantiation
    private AccountNumberGenerator() {
    }

    // Public getInstance method to provide access to the single instance
    public static synchronized AccountNumberGenerator getInstance() {
        if (instance == null) {
            instance = new AccountNumberGenerator();
        }
        return instance;
    }

    // Synchronized method to get the next account number
    public synchronized int getNextNumber() {
        return nextAccountNumber++;
    }
}

public class AccountNumberGeneratorDemo {
    public static void main(String[] args) {
        // Create multiple threads to access the AccountNumberGenerator
        Thread thread1 = new Thread(() -> {
            AccountNumberGenerator generator = AccountNumberGenerator.getInstance();
            int accountNumber = generator.getNextNumber();
            System.out.println("Thread 1: Account Number " + accountNumber);
        });

        Thread thread2 = new Thread(() -> {
            AccountNumberGenerator generator = AccountNumberGenerator.getInstance();
            int accountNumber = generator.getNextNumber();
            System.out.println("Thread 2: Account Number " + accountNumber);
        });

        thread1.start();
        thread2.start();
    }
}
