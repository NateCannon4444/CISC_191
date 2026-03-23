# DrugItem Class
```Java
class DrugItem {
    protected String name;
    protected String companyName;

    public DrugItem() {
        this.name = "";
        this.companyName = "";
    }

    public void updateInfo(String name, String companyName) {
        this.name = name;
        this.companyName = companyName;
    }

    public void display() {
        System.out.print("Item: " + name + "Company: " + companyName);
    }
}
```
# Painkiller Class
```Java
class Painkiller extends DrugItem {
    private String expiryDate;
    private String ageGroup;

    @Override
    public void display() {
        super.display();
        System.out.println(" Expiry: " + expiryDate + " Age: " + ageGroup);
    }

    public void updatePainkiller(String name, String company, String expiry, String age) {
        updateInfo(name, company);
        this.expiryDate = expiry;
        this.ageGroup = age;
    }
}
```
# Bandage Class
```Java
class Bandage extends DrugItem {
    private String expiryDate;
    private String ageGroup;
    private boolean isWaterproof;

    @Override
    public void display() {
        super.display();
        System.out.println(" Expiry: " + expiryDate + " Age: " + ageGroup + " Waterproof: " + (isWaterproof ? "Y" : "N"));
    }

    public void updateBandage(String name, String company, String expiry, String age, boolean waterproof) {
        updateInfo(name, company);
        this.expiryDate = expiry;
        this.ageGroup = age;
        this.isWaterproof = waterproof;
    }
}

```
# Equiptment Class
```Java
class Equipment extends DrugItem {
    private double weight;

    public void updateEquipment(String name, String company) {
        updateInfo(name, company);
    }

    public void updateEquipment(String name, String company, double weight) throws InvalidWeightException {
        if (weight < 0) throw new InvalidWeightException("weight cannot be negative");
        updateInfo(name, company);
        this.weight = weight;
    }

    @Override
    public void display() {
        super.display();
        System.out.println(" Weight: " + weight + " lbs");
    }
}
```
# Custom Exception Class
```Java
//Used for Version 3
class InvalidWeightException extends Exception {
    public InvalidWeightException(String message) {
        super(message);
    }
}
```
# Main Class
```Java
import java.util.ArrayList;
import java.util.Scanner;

public class Main {
    private static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        ArrayList<DrugItem> inventory = new ArrayList<>();
        boolean adding = true;

        while (adding) {
            System.out.println("\nSelect item type to add:");
            System.out.println("1. Painkiller\n2. Bandage\n3. Equipment\n4. Exit and Show Inventory");   
            //Version 2: Catching number exceptions
            int choice = getValidInt("Choice: ");
            switch (choice) {
                case 1:
                    Painkiller pk = new Painkiller();
                    System.out.print("Enter Name: ");
                    String pkName = scanner.nextLine();
                    System.out.print("Enter Company: ");
                    String pkComp = scanner.nextLine();
                    System.out.print("Enter Expiry (MM/YY): ");
                    String pkExp = scanner.nextLine();
                    System.out.print("Enter Age Group: ");
                    String pkAge = scanner.nextLine();
                    
                    pk.updatePainkiller(pkName, pkComp, pkExp, pkAge);
                    inventory.add(pk);
                    break;

                case 2:
                    Bandage bd = new Bandage();
                    System.out.print("Enter Name: ");
                    String bdName = scanner.nextLine();
                    System.out.print("Enter Company: ");
                    String bdComp = scanner.nextLine();
                    System.out.print("Enter Expiry (MM/YY): ");
                    String bdExp = scanner.nextLine();
                    System.out.print("Enter Age Group: ");
                    String bdAge = scanner.nextLine();
                    System.out.print("Is it Waterproof? (true/false): ");
                    boolean bdWater = Boolean.parseBoolean(scanner.nextLine());
                    
                    bd.updateBandage(bdName, bdComp, bdExp, bdAge, bdWater);
                    inventory.add(bd);
                    break;

                case 3:
                    Equipment eq = new Equipment();
                    System.out.print("Enter Name: ");
                    String eqName = scanner.nextLine();
                    System.out.print("Enter Company: ");
                    String eqComp = scanner.nextLine();
                    
                    //Version 3:Catching custom exception (InvalidWeightException)
                    try {
                        double eqWeight = getValidDouble("Enter Weight (lbs): ");
                        eq.updateEquipment(eqName, eqComp, eqWeight);
                        inventory.add(eq);
                    } catch (InvalidWeightException e) {
                        System.out.println("Custom Error Caught: " + e.getMessage());
                    }
                    break;

                case 4:
                    adding = false;
                    break;

                default:
                    System.out.println("Invalid selection. Try again.");
            }
        }

        System.out.println("\n--- Final Inventory List ---");
        for (DrugItem item : inventory) {
            item.display();
        }
        
        scanner.close();
    }
    // Used for Version 2
    public static int getValidInt(String prompt) {
        while (true) {
            try {
                System.out.print(prompt);
                return Integer.parseInt(scanner.nextLine());
            } catch (NumberFormatException e) {
                System.out.println("Error: Please enter a valid whole number.");
            }
        }
    }
    // Used for Version 2
    public static double getValidDouble(String prompt) {
        while (true) {
            try {
                System.out.print(prompt);
                return Double.parseDouble(scanner.nextLine());
            } catch (NumberFormatException e) {
                System.out.println("Error: Please enter a numeric value (e.g., 10.5).");
            }
        }
    }
}
```
