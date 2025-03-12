# Store-stock-management-system
import java.util.Scanner;

class Main1321 
{
    static String RESET = "\033[0m";//Reset
    static String BOLD = "\033[1m";//Bold
    static String UNDERLINE = "\033[4m";//Underline

    static String savedUsername = "";
    static String savedPassword = "";

    public static void main(String[] args) 
	{
        Scanner sc = new Scanner(System.in);

        System.out.println(UNDERLINE + BOLD + "\t\t\t*********** Welcome To The ************" + RESET);
        System.out.println(BOLD + "\t\t\t======================================" + RESET);
        System.out.println("\t\t\t" + BOLD + "      Store Stock Management System    " + RESET);
        System.out.println(UNDERLINE + BOLD + "\t\t\t======================================\n" + RESET);

        while (true) 
		{
            System.out.println(BOLD + "\t\t\t1. Signup" + RESET);
            System.out.println(BOLD + "\t\t\t2. Login" + RESET);
            System.out.println(BOLD + "\t\t\t3. Exit" + RESET);
            System.out.print("\n\t\t\tEnter your choice: ");
            
            int choice = sc.nextInt();
            sc.nextLine();

            switch (choice) 
			{
                case 1:
                    signup(sc);
                    break;
                case 2:
                    if (login(sc)) 
					{
                        storeManagementSystem(sc);
                    }
                    break;
                case 3:
                    System.out.println(BOLD + UNDERLINE + "\n\t\t\tExiting system...\n" + RESET);
                    System.exit(0);
                default:
                    System.out.println("\n\t\t\tInvalid choice! Please try again.\n");
            }
        }
    }

    static void signup(Scanner sc) 
	{
        System.out.print("\t\t\tEnter a username: ");
        savedUsername = sc.nextLine();
        System.out.print("\t\t\tEnter a password: ");
        savedPassword = sc.nextLine();
        System.out.println("\n\t\t\tSignup successful! Now you can log in.\n");
    }

    static boolean login(Scanner sc) 
	{
        System.out.print("\t\t\tEnter username: ");
        String username = sc.nextLine();
        System.out.print("\t\t\tEnter password: ");
        String password = sc.nextLine();

        if (username.equals(savedUsername) && password.equals(savedPassword)) 
		{
            System.out.println("\n\t\t\tLogin successful! Welcome, " + username + "!\n");
            return true;
        } 
		else 
		{
            System.out.println("\n\t\t\tInvalid username or password. Try again.\n");
            return false;
        }
    }

    static void storeManagementSystem(Scanner sc)
	{
        Store store = new Store(100);

        while (true) 
		{
            System.out.println(BOLD + "\t\t\t1. Add Product" + RESET);
            System.out.println(BOLD + "\t\t\t2. Remove Product" + RESET);
            System.out.println(BOLD + "\t\t\t3. Update Quantity" + RESET);
            System.out.println(BOLD + "\t\t\t4. Display All Products" + RESET);
            System.out.println(BOLD + "\t\t\t5. Sell Product" + RESET);
            System.out.println(BOLD + "\t\t\t6. Show Most Sold Product" + RESET);
            System.out.println(BOLD + "\t\t\t7. Logout" + RESET);
            System.out.print("\n\t\t\tEnter your choice: ");

            int choice = sc.nextInt();
            sc.nextLine();
            System.out.println();

            switch (choice) {
                case 1:
                    System.out.print("\t\t\tEnter product name: ");
                    String name = sc.nextLine();
                    System.out.print("\t\t\tEnter product price: Rs : ");
                    double price = sc.nextDouble();
                    System.out.print("\t\t\tEnter product quantity: ");
                    int quantity = sc.nextInt();
					sc.nextLine();
					System.out.print("\t\t\tEnter discription : ");
					String disc = sc.nextLine();

                    Product product = new Product(name, price, quantity,disc);
                    store.addProduct(product);
                    System.out.println(BOLD + "\n\t\t\tProduct added successfully!\n" + RESET);
                    break;

                case 2:
                    System.out.print("\t\t\tEnter product name to remove: ");
                    String removeName = sc.nextLine();
                    store.removeProduct(removeName);
                    break;

                case 3:
                    System.out.print("\t\t\tEnter product name to update: ");
                    String updateName = sc.nextLine();
                    System.out.print("\t\t\tEnter new quantity: ");
                    int newQuantity = sc.nextInt();
                    store.updateQuantity(updateName, newQuantity);
                    break;

                case 4:
                    store.displayAllProducts();
                    break;

                case 5:
                    System.out.print("\t\t\tEnter product name to sell: ");
                    String sellName = sc.nextLine();
                    System.out.print("\t\t\tEnter quantity to sell: ");
                    int sellQuantity = sc.nextInt();
                    store.sellProduct(sellName, sellQuantity);
                    break;

                case 6:
                    store.showMostSoldProduct();
                    break;

                case 7:
                    System.out.println(BOLD + "\n\t\t\tLogging out...\n" + RESET);
                    return;

                default:
                    System.out.println("\n\t\t\tInvalid choice! Please try again.\n");
            }
        }
    }
}
class Product 
{
	static String RESET = "\033[0m";//Reset
    static String BOLD = "\033[1m";//Bold
    static String UNDERLINE = "\033[4m";//Underline
    String name;
    double price;
    int quantity;
	String discription;

    Product(String name, double price, int quantity,String disc) 
	{
        this.name = name;
        this.price = price;
        this.quantity = quantity;
		this.discription=disc;
    }

    void displayProduct() 
	{
        String price1 = String.format("%.2f", price);
        System.out.printf("\n\t\t\t%-13s \t%11s \t%9s \t%11s", name, price1, quantity,discription);
    }
}


class Store {
	static String RESET = "\033[0m";//Reset
    static String BOLD = "\033[1m";//Bold
    static String UNDERLINE = "\033[4m";//Underline
    Product[] products;
    int productCount;
    String mostSoldProduct;
    int mostSoldQuantity;

    Store(int size) 
	{
        products = new Product[size];
        productCount = 0;
        mostSoldProduct = "";
        mostSoldQuantity = 0;
    }
   void addProduct(Product product) 
   {
        if (productCount < products.length) 
		{
            products[productCount++] = product;
        } 
		else 
		{
            System.out.println("\n\t\t\tStore is full! Cannot add more products.\n");
        }
    }
  void removeProduct(String productName) 
  {
        for (int i = 0; i < productCount; i++) 
		{
            if (products[i].name.equalsIgnoreCase(productName)) 
			{
                for (int j = i; j < productCount - 1; j++) 
				{
                    products[j] = products[j + 1];
                }
                products[--productCount] = null;
                System.out.println("\n\t\t\tProduct '" + productName + "' removed successfully.\n");
                return;
            }
        }
        System.out.println("\n\t\t\tProduct not found!\n");
    }

    void updateQuantity(String productName, int newQuantity) 
	{
        for (int i = 0; i < productCount; i++) 
		{
            if (products[i].name.equalsIgnoreCase(productName)) 
			{
                products[i].quantity = newQuantity;
                System.out.println("\n\t\t\tQuantity of '" + productName + "' updated to " + newQuantity + ".\n");
                return;
            }
        }
        System.out.println("\n\t\t\tProduct not found!\n");
    }
  
    void sellProduct(String productName, int quantity) 
	{
        for (int i = 0; i < productCount; i++) 
		{
            if (products[i].name.equalsIgnoreCase(productName)) 
			{
                if (products[i].quantity >= quantity) 
				{
                    products[i].quantity -= quantity;
                    
					if (quantity > mostSoldQuantity)
					{
                        mostSoldQuantity += quantity;
                        mostSoldProduct = productName;
                    }
                    System.out.println("\n\t\t\tProduct sold successfully!\n");
                } 
				else 
				{
                    System.out.println("\n\t\t\tNot enough stock available!\n");
                }
                return;
            }
        }
        System.out.println("\n\t\t\tProduct not found!\n");
    }

    void showMostSoldProduct()
	{
        System.out.println("\n\t\t\tMost Sold Product: " + mostSoldProduct + " (" + mostSoldQuantity + " units)\n");
    }
  void displayAllProducts() 
	{
        if (productCount == 0) 
		{
            System.out.println(BOLD+"\n\t\t\tNo products in stock!\n"+RESET);
        }
		else
		{
            System.out.println("\n\t\t\t===============================");
            System.out.println(BOLD+UNDERLINE+"\t\t\tProducts in Stock:"+RESET);
            System.out.println("\t\t\t===============================\n");
            System.out.println("\t\t\t------------------------------------------------------------");
            System.out.printf(BOLD+"\n\t\t\t%-13s \t%13s \t%13s \t%11s\n", "Product Name", "Price (in Rs.)", "Quantity","Discription"+RESET);

            for (int i = 0; i < productCount; i++) 
			{
                products[i].displayProduct();
            }
            System.out.println("\n\t\t\t------------------------------------------------------------");
        }
    }
}
