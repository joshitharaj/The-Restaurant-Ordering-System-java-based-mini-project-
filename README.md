# The-Restaurant-Ordering-System-java-based-mini-project

import java.util.ArrayList;
	import java.util.List;
	import java.util.Scanner;


	class MenuItem {
	    private String name;
	    private double price;

	    public MenuItem(String name, double price) {
	        this.name = name;
	        this.price = price;
	    }

	    public String getName() {
	        return name;
	    }

	    public double getPrice() {
	        return price;
	    }
	}

	class OrderItem {
	    private MenuItem menuItem;
	    private int quantity;

	    public OrderItem(MenuItem menuItem, int quantity) {
	        this.menuItem = menuItem;
	        this.quantity = quantity;
	    }

	    public MenuItem getMenuItem() { 
	        return menuItem;
	    }

	    public int getQuantity() {
	        return quantity;
	    }
	}

	public class RestaurantOrderingSystem {
		public static void main(String[] args) {
	        Scanner scanner = new Scanner(System.in);
	        List<MenuItem> menuItems = createMenu();
	        List<OrderItem> orderItems = new ArrayList<>();

	        System.out.println("\n*Welcome to the Restaurant Ordering System!*");

	        while (true) {
	            System.out.println("\nMENU:");
	            for (int i = 0; i < menuItems.size(); i++) {
	                System.out.println((i + 1) + ". " + menuItems.get(i).getName() + " - RS." + menuItems.get(i).getPrice());
	            }

	            System.out.println("0. Place Order");
	            System.out.println("-1. Exit");
	            System.out.print("Select an item: ");
	            int choice = scanner.nextInt();

	            if (choice == -1) {
	                break;
	            } else if (choice == 0) {
	                viewOrder(orderItems);
	                break;
	            } else if (choice > 0 && choice <= menuItems.size()) {
	                System.out.print("Enter quantity: ");
	                int quantity = scanner.nextInt();
	                MenuItem selectedItem = menuItems.get(choice - 1);
	                orderItems.add(new OrderItem(selectedItem, quantity));
	                System.out.println("Added to order: " + quantity + "x " + selectedItem.getName());
	            } else {
	                System.out.println("Invalid choice.");
	            }
	        }

	        scanner.close();
	    }

	    private static List<MenuItem> createMenu() {
	        List<MenuItem> menuItems = new ArrayList<>();
	        menuItems.add(new MenuItem("Burger", 250.55));
	        menuItems.add(new MenuItem("Pizza", 395.15));
	        menuItems.add(new MenuItem("Pasta", 199.99));
	        menuItems.add(new MenuItem("Salad", 159.34));
	        return menuItems;
	    }

	    private static void viewOrder(List<OrderItem> orderItems) {
	    	System.out.println("\n*");
	        System.out.println("Your Order :");
	        double total = 0;
	        for (OrderItem orderItem : orderItems) {
	            MenuItem menuItem = orderItem.getMenuItem();
	            int quantity = orderItem.getQuantity();
	            double subtotal = menuItem.getPrice() * quantity;
	            System.out.println(quantity + "x " + menuItem.getName() + " - RS " +  subtotal);
	            total += subtotal;
	        }
	        System.out.println("The Total is: RS " +  total);
	        double gstRate = 0.10;
	        double gstAmount = total * gstRate;
	        
	        // Calculate the total cost including GST
	        double totalCostWithGST = total + gstAmount;
	        
	        System.out.println("\n~~");
	        System.out.println(" KING HOTEL");
	        System.out.println("--- Bill ---");
	        
	        System.out.println("Subtotal: RS " + total);
	        System.out.println("GST (" + (gstRate * 100) + "%): Rs" + gstAmount);
	        System.out.println("Total: RS " + totalCostWithGST);
	    }
	   
	

}
