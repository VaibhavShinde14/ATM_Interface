import java.util.Scanner;
class InterfaceOfAtm {
    String name;
    String userName;
    String password;
    String accountNo;
    double balance = 500000.00;
    int transactions = 0;
    String transactionHistory = "";
// User Registration
public void register() {
    Scanner sc = new Scanner(System.in);
    System.out.println("Enter your name : ");
    this.name = sc.nextLine();
    System.out.println("\nEnter Username: ");
    this.userName = sc.nextLine();
    System.out.println("\nEnter the Password: ");
    this.password = sc.nextLine();
    System.out.println("\nEnter your Account Number: ");
    this.accountNo = sc.nextLine();
    System.out.println("\nRegistration completed successfully! Kindly login to your Account.");
}
// User Login
public boolean login() {
    boolean isLogin = false;
    Scanner Sc= new Scanner(System.in);
    while (!isLogin) {
        System.out.print("\nEnter Username: ");
        String username = Sc.nextLine();
        if (username.equals(userName)) {
            while (!isLogin) {
                System.out.print("\nEnter Your Password : ");
                String Password = Sc.nextLine();
                if (Password.equals(password)) {
                    System.out.println("\nLogin successfull!");
                    isLogin = true;
                } else
                    System.out.println("\neIncorrect Password. Please Check Again");
            }
        } else
            System.out.println("\n#Sorry! Username not found#");
    }
    return isLogin;
}
// withdraw money
public void withdraw() {
    System.out.println("\nEnter the amount to be withdrawn: ");
    Scanner sc = new Scanner (System.in);
    double amount = sc.nextDouble();
    try {
        if (balance >= amount) {
            balance -= amount;
            System.out.println("\nSucessfully Withdrawn! " + amount + "Rs");
            String str = "Rs " + amount + "Withdrawn\n";
            transactionHistory = transactionHistory.concat(str);
        } else
            System.out.println("\nBalance is Insufficient.");
    } catch (Exception e) { 
    }
}
// Deposit
public void deposit() {
    System.out.println("\nEnter the amount you want to deposit : ");
    Scanner sc = new Scanner(System.in);
    double amount = sc.nextDouble();
    try {
        if (amount <= 100000.00) {
            transactions++;
            balance += amount;
            System.out.println("\nDeposit" + amount +  "Rs successfully");
            String str = "Rs " + amount + " deposited\n";
            transactionHistory = transactionHistory.concat(str);
        } else
            System.out.println("\nLimit Exceeded!");
    } catch (Exception e) {
    }
}
// Transfer
public void transfer() {
    Scanner s = new Scanner(System.in);
    System.out.println("\nEnter recepient name: ");
    String recepient = s.nextLine();
    System.out.println("\nEnter amount to be transferred: ");
    double amount = s.nextDouble();
    try {
        if (balance >= amount) {
            if (amount <= 40000.00) {
                transactions++;
                balance -= amount;
                System.out.println("\nSuccessfully transferred to " + recepient);
                String str = "Rs " + amount + " transferred to " + recepient + "\n";
                transactionHistory = transactionHistory.concat(str);
        } else
            System.out.println("\nSorry! Limit is 40000.00");
    } else
        System.out.println("\nBalance is Insufficient. Please check your balance first!");
    } catch (Exception e) {
    }
}
// Check balance
public void checkBalance() {
    System.out.println("\nRs " + balance);
}
// transaction history
public void transHistory () {
    if (transactions == 0)
        System.out.println("\nEmpty!");
    else
        System.out.println("\n" + transactionHistory);
    }
}
// Interface of ATM
class ATM_Interface {
    public static int Interface() {
        int input = 0;
        boolean flag = false;
        while (!flag) {
            try {
                Scanner sce = new Scanner(System.in);
                input = sce.nextInt(); 
                flag = true;
                if (flag && input > 2 || input < 1) {
                    System.out.println("Select the number between 1 or 2" );
                    flag = false;
                }
            } catch (Exception e) {
                System.out.println("Enter integer value only");
                flag = false;
            }
        }
        ;
      return input;
}
// main method

public static void main(String[] args) {
    System.out.println("\n WELCOME TO SBI ATM \n");
    System.out.println("1. Register\n2. Exit");
    Scanner xp = new Scanner(System.in);
    System.out.print("Enter your choice: ");
    int choice = xp.nextInt();
    if (choice == 1) {
    InterfaceOfAtm b = new InterfaceOfAtm();
    b.register();
    while (true) {
        System.out.println("\n1.Login\n2.Exit");
        System.out.print ("Enter your choice : ");
        int ch = xp.nextInt();
        if (ch == 1) {
            if (b.login()) {
                System.out.println(" \n\n WELCOME BACK!" + b.name + "\n\n");
                boolean isFinished = false;
                while (!isFinished) {
                System.out.println("\n1.Deposit\n2.withdraw\n3.Transfer\n4.Transaction History\n5.Check Balance");
                System.out.print("Enter your choice: ");
                int c = xp.nextInt();
                switch (c) {
                    case 1:
                        b.deposit();
                        break;
                    case 2:
                        b.withdraw();
                        break;
                    case 3:
                        b.transfer();
                        break;
                    case 4:
                        b.transHistory();
                        break;
                    case 5:
                        b.checkBalance();
                        break;
                    case 6:
                        isFinished = true;
                        break;
                    default:
                        System.out.println("\nwrong Choice!");
                }
            }
        }
    }else
        System.out.println("Wrong Choice");
    }
} else
    System.out.println("Wrong Choice");
}
}
