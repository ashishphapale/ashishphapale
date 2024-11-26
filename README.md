package defaultpackage;

import java.util.Scanner;

class InventoryItem {
    private String name;
    private int quantity;

    public InventoryItem(String name, int quantity) {
        this.name = name;
        this.quantity = quantity;
    }

    public String getName() {
        return name;
    }

    public int 
 getQuantity() {
        return quantity;
    }

    public void setQuantity(int quantity) {
        this.quantity = quantity;
    }
}

     
 class InventoryManagementSystem {
    
 static InventoryItem[] inventory = new InventoryItem[100]; 
    private static int itemCount = 0;

    public static void addItem(String name, int quantity) {
        try {
            if (quantity <= 0) {
                throw new IllegalArgumentException("Quantity must be positive.");
            }
            try {
				try {
					if (itemCount >= inventory.length) {
					    throw new IndexOutOfBoundsException("Inventory is full.");
					}
				} catch (Exception e) {
					
					e.printStackTrace();
				}
			} catch (Exception e) {
			
				e.printStackTrace();
			}
            inventory[itemCount] = new InventoryItem(name, quantity);
            itemCount++;
            System.out.println(name + " added to inventory with " + quantity + " units.");
        } catch (IllegalArgumentException | IndexOutOfBoundsException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }

    public static void searchItem(String name) {
        for (int i = 0; i < itemCount; i++) {
            if (inventory[i].getName().equals(name)) {
                System.out.println("Item " + name + " found in inventory with " + inventory[i].getQuantity() + " units.");
                return;
            }
        }
        System.out.println("Item " + name + " not found in inventory.");
    }

    public static void modifyItem(String name, int newQuantity) {
        try {
            if (newQuantity <= 0) {
                throw new IllegalArgumentException("New quantity must be positive.");
            }
            for (int i = 0; i < itemCount; i++) {
            
                if (inventory[i].getName().equals(name)) {
                    inventory[i].setQuantity(newQuantity);
                    System.out.println("Quantity of " + name + " updated to " + newQuantity);
                    return;
                }
            }
            System.out.println("Item " + name + " not found in inventory.");
        } catch (IllegalArgumentException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in); 


        int choice;
        String item;
        int quantity;

        do {
            System.out.println("Inventory Management System");
            System.out.println("1. Add Item");
            System.out.println("2. Search Item");
            System.out.println("3. Modify Item");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            choice = sc.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter item name: ");
                    item = sc.next();
                    System.out.print("Enter quantity: ");
                    quantity = sc.nextInt();
                    addItem(item, quantity);
                    break;
                case 2:
                    System.out.print("Enter item name to search: ");
                    item = sc.next();
                    searchItem(item);
                    break;
                case 3:
                    System.out.print("Enter item name to modify: ");
                    item = sc.next();
                    System.out.print("Enter new quantity: ");
                    quantity = sc.nextInt();
                    modifyItem(item, quantity);
                    break;
                case 4:
                    System.out.println("Exiting inventory management system.");
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");  

            }
        } while (choice != 4);

        sc.close();
    }
    }
