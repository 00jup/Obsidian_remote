# before refactoring
## BankApplication.java

```java
import java.util.Scanner;
import java.util.ArrayList;

public class BankApplication {
    private static ArrayList<Account> accounts = new ArrayList<>();

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\n1. 계좌 생성 2. 계좌 목록 3. 예금 4. 출금 5. 종료");
            System.out.print("선택> ");
            int selection = scanner.nextInt();
            scanner.nextLine();  // 숫자 입력 후 엔터 처리

            switch (selection) {
                case 1:
                    createAccount(scanner);
                    break;
                case 2:
                    listAccounts();
                    break;
                case 3:
                    processDeposit(scanner);
                    break;
                case 4:
                    processWithdraw(scanner);
                    break;
                case 5:
                    System.out.println("프로그램을 종료합니다.");
                    return;
                default:
                    System.out.println("올바른 번호를 선택해주세요.");
                    break;
            }
        }
    }

    private static void createAccount(Scanner scanner) {
        System.out.print("계좌번호: ");
        String num = scanner.nextLine();
        System.out.print("계좌주: ");
        String owner = scanner.nextLine();
        System.out.print("초기금액: ");
        int initialBalance = scanner.nextInt();
        scanner.nextLine();  // 숫자 입력 후 엔터 처리

        Account newAccount = new Account(num, owner, initialBalance);
        accounts.add(newAccount);
        System.out.println("계좌가 생성되었습니다.");
    }

    private static void listAccounts() {
        for (Account acc : accounts) {
            System.out.println(acc);
        }
    }

    private static void processDeposit(Scanner scanner) {
        System.out.print("계좌번호: ");
        String num = scanner.nextLine();
        Account account = findAccount(num);
        if (account != null) {
            System.out.print("예금액: ");
            int amount = scanner.nextInt();
            scanner.nextLine();  // 숫자 입력 후 엔터 처리
            account.deposit(amount);
            System.out.println("예금 처리가 완료되었습니다.");
        } else {
            System.out.println("계좌를 찾을 수 없습니다.");
        }
    }

    private static void processWithdraw(Scanner scanner) {
        System.out.print("계좌번호: ");
        String num = scanner.nextLine();
        Account account = findAccount(num);
        if (account != null) {
            System.out.print("출금액: ");
            int amount = scanner.nextInt();
            scanner.nextLine();  // 숫자 입력 후 엔터 처리
            account.withdraw(amount);
            System.out.println("출금 처리가 완료되었습니다.");
        } else {
            System.out.println("계좌를 찾을 수 없습니다.");
        }
    }

    private static Account findAccount(String accountNum) {
        for (Account acc : accounts) {
            if (acc.getAccountNum().equals(accountNum)) {
                return acc;
            }
        }
        return null;
    }
}
```

## Account.java
```java
public class Account {
    private String accountNum;
    private String name;
    private int balance;

    public Account() {}

    public Account(String accountNum, String name, int initialBalance){
        this.accountNum = accountNum;
        this.name = name;
        this.balance = initialBalance;
    }

    public void deposit(int amount){
        if (amount > 0) {
            balance += amount;
        } else {
            System.out.println("입금액은 양수여야 합니다.");
        }
    }

    public void withdraw(int amount){
        if (amount <= balance) {
            balance -= amount;
        } else {
            System.out.println("잔액이 부족합니다.");
        }
    }

    public String getAccountNum() {
        return accountNum;
    }

    public String getName() {
        return name;
    }

    public int getBalance() {
        return balance;
    }

    @Override
    public String toString() {
        return accountNum + " " + name + " 잔액: " + balance;
    }
}

```

# after refactoring
## BankApplication.java

```java
package ch04.sec02;
import java.util.Scanner;

public class BankApplication {
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        int selection;

        account new_account[] = new account[100];
        for(int i = 0; i<100; i++)
            new_account[i] = new account();

        String account_num;
        String name;
        int total_money;
        int i = 0;
        while(true){
            System.out.print("1. 계좌 생성 2. 계좌목록 3. 예금 4. 출금 5. 종료\n 선택>");
            selection = scan.nextInt();
            scan.nextLine();
            switch (selection){
                case 1:
                    System.out.print("1. 계좌번호: ");
                    account_num = scan.nextLine();
                    System.out.print("2. 계좌주: ");
                    name = scan.nextLine();
                    System.out.print("3. 초기금액: ");
                    total_money = scan.nextInt();
                    scan.nextLine();
                    new_account[i++] = new account(account_num, name, total_money);
                    System.out.print("계좌가 생성되었습니다.\n");
                    break;
                case 2:
                    for(int j =0; j<i; j++)
                        System.out.println(new_account[j].account_num + "  " + new_account[j].name+"  " + new_account[j].total_money);
                    break;
                case 3:
                    System.out.print("계좌번호: ");
                    account_num = scan.nextLine();
                    System.out.print("예금액: ");
                    total_money = scan.nextInt();
                    scan.nextLine();
                    for(int j =0; j<i; j++){
                        if (new_account[j].account_num.equals(account_num)){
                            new_account[j].deposit(total_money);
                            System.out.println(new_account[j].total_money);
                            break;
                        }
                    }
                    break;
                case 4:
                    System.out.print("계좌번호: ");
                    account_num = scan.nextLine();
                    System.out.print("출금액: ");
                    total_money = scan.nextInt();
                    scan.nextLine();
                    for(int j =0; j<i; j++){
                        if (new_account[j].account_num.equals(account_num)){
                            new_account[j].draw(total_money);
                            System.out.println(new_account[j].total_money);
                            break;
                        }
                    }
                    break;
                case 5:
                    break;
            }
        }



    }
}

```

## Account.java
```java
package ch04.sec02;

public class account {
    String account_num;
    String name;
    int total_money;
    account(){}



    account(String account_num, String name, int total_money){
        this.account_num = account_num;
        this.name = name;
        this.total_money = total_money;
    }

    void deposit(int deposit_money){
        this.total_money += deposit_money;
    }
    void draw(int draw_money){
        this.total_money -= draw_money;
    }

}

```