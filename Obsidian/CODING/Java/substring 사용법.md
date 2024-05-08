

```java
import java.util.Scanner;

public class NucleicSequences {

    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        System.out.println("Write the necleic sequences >>");
        String sequences = scanner.nextLine();
        String[] SeqArr = sequences.split(",");

        for (int i = 0; i < SeqArr.length; i++) {

            if (SeqArr[i].length() < 9)
                System.out.println("Genome " + i + ": Not sufficient length");

            else {
                String substr = SeqArr[i].substring(3, 9);
                boolean result = substr.contains("ATC");
                if (SeqArr[i].charAt(0) == 'G' && result) {
                    System.out.println("Genome " + i + ": Positive");
                } else
                    System.out.println("Genome " + i + ": Negative");
            }
        }

        scanner.close();
    }

}

```

여기서 substring은 정말로 index를 나타내는 것임.