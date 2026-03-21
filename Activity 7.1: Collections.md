# PalindromeCheck class
```Java
import java.util.ArrayDeque;
import java.util.Deque;
import java.util.Scanner;

public class PalindromeCheck {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Enter text:");
        String input = scanner.nextLine();
        
        if (isPalindrome(input)) {
            System.out.println("Yes, " + input + " is a palindrome.");
        } else {
            System.out.println("No, \"" + input + "\" is not a palindrome.");
        }
        
        scanner.close();
    }

    public static boolean isPalindrome(String text) {
        String cleaned = text.toLowerCase().replaceAll("[^a-z]", "");
        if (cleaned.length() <= 1) {
            return true;
        }
        Deque<Character> deque = new ArrayDeque<>();

        for (char ch : cleaned.toCharArray()) {
            deque.addLast(ch);
        }

        while (deque.size() > 1) {
            Character front = deque.removeFirst();
            Character back = deque.removeLast();
            
            if (!front.equals(back)) {
                return false;
            }
        }

        return true;
    }
}
```
