# Supermarket Billing System

A simple Python-based supermarket billing system that simulates a basic shopping experience in a supermarket. The system allows customers to add items to their cart, view a menu with item prices, and generate a detailed receipt with applied discounts based on the total amount. This project is implemented using Python, demonstrating fundamental programming concepts such as loops, functions, dictionaries, and input handling.

## Features

- **Menu Display:** Shows a list of available items and their prices.
- **Cart Management:** Allows customers to add multiple items to the cart, with quantities specified for each item.
- **Receipt Generation:** Prints a detailed receipt that includes item names, quantities, prices, subtotal, discount (if applicable), and the final total.
- **Discount Calculation:** Automatically applies a discount based on the total purchase amount:
  - 10% discount for purchases over 1000 INR.
  - 5% discount for purchases over 500 INR.
- **Modular Code Structure:** The code is organized into functions for better readability and maintenance.

## How to Run the Program

1. **Requirements:** Make sure you have Python installed on your system (Python 3.6 or higher is recommended).
2. **Run the Code:** Execute the code in a Python environment (e.g., Jupyter Notebook, VS Code, or directly from the command line).
3. **Follow the Prompts:** The program will prompt you to enter your name, phone number, and then add items to your cart. After adding items, you can print the receipt to see the final bill.

## Source Code

Below is the complete Python code for the supermarket billing system:

```python
# Executes for every new customer
while True:
    print("-"*45)
    print("Welcome to the Super Market Billing System")
    print("-"*45)

    #Asks name & phone number of the customer
    name = input("Enter your name:\n")
    phone = int(input("Enter your phone number:\n"))

    # Dictionary of menu items from the super market store
    menu_items = {
        "Apple": 40.0,
        "Banana": 20.0,
        "Orange": 50.0,
        "Bread": 30.0,
        "Milk": 25.0,
        "Eggs": 60.0,
        "Chicken Breast": 300.0,
        "Rice": 90.0,
        "Pasta": 75.0,
        "Tomato": 30.0,
        "Onion": 20.0,
        "Potato": 25.0,
        "Butter": 50.0,
        "Cheese": 200.0,
        "Yogurt": 40.0,
        "Coffee": 250.0,
        "Tea": 150.0,
        "Chocolate": 80.0,
        "Cereal": 180.0,
        "Detergent": 250.0
    }

    print("-"*45)
    print("MENU ITEMS & PRICE (INR)")
    print("-"*45)

    # Prints the menu for the customer
    for i, j in menu_items.items():
        print("{:<15} {:<13}".format(i, j))

    print("-"*45)

    amount = 0
    discount = 0
    final_amount = 0
    cart = {}

    # Loop used for adding items to the cart of the customer
    while True:
        flag = 0

        # Asks customer for item name
        item_name = input("Enter item name:").title()
        for item, cost in menu_items.items():
            if item_name == item:
                flag = 1
                break

        # Checks if item name is invalid 
        if flag == 0:
            print("Invalid item name")
            continue

        # Asks item quantity from the user
        quantity = int(input("Enter quantity:"))

        # Adds quantity to the dictionary
        if item_name in cart:
            cart[item_name] += quantity  # Increment existing quantity
        else:
            cart[item_name] = quantity  # Add new item with its quantity

        # Calculates initial amount
        amount += menu_items[item_name] * quantity

        # Asks customer to press 1 if more items are to be added to the cart or
        # Press 2 to print the Receipt
        # Anything other than 1 or 2 is considered as invalid input and user is requested to re-enter the input
        while True:
            add_items = input("""Press 1 to add more items \nPress 2 to print the Receipt\n""")

            if add_items not in ("1", "2"):
                print("Enter valid input")
            else:
                break

        # If customer does not want to add more items, the receipt gets printed
        if add_items == "2":
            print("\n")
            print("-"*18, "Receipt", "-"*18)
            print("Name:", name)
            print("Phone Number:", phone)
            print("-"*45)
            # Prints Headers (Item, Quantity, Price, Total)
            print("{:<15} {:<11} {:<9} {:<12}".format("Item", "Quantity", "Price", "Total"))
            print("-"*45)
            # Prints Items from the cart
            for x, y in cart.items():
                print("{:<15} {:<11} {:<9} {:<12}".format(x, y, menu_items[x], y * menu_items[x]))
            print("-"*45)
            # Prints initial amount
            print("Subtotal:", amount)

            # Calculates discount
            if amount >= 1000:
                discount += amount * 0.1
                per = 10
            elif amount >= 500:
                discount += amount * 0.05
                per = 5
            else:
                discount = 0
                per = 0
            print(f"Discount({per}%): -{discount}")

            # Calculates final amount
            final_amount = amount - discount
            print("Total Amount:", final_amount)

            print("-"*45)
            print("\n\n")
            break
```

## Example Output

```
---------------------------------------------
Welcome to the Super Market Billing System
---------------------------------------------
Enter your name:
John
Enter your phone number:
9876543210
---------------------------------------------
MENU ITEMS & PRICE (INR)
---------------------------------------------
Apple           40.0        
Banana          20.0        
...
---------------------------------------------
Enter item name: Apple
Enter quantity: 2
Press 1 to add more items 
Press 2 to print the Receipt
2

------------------ Receipt ------------------
Name: John
Phone Number: 9876543210
---------------------------------------------
Item            Quantity    Price     Total     
---------------------------------------------
Apple           2           40.0      80.0      
---------------------------------------------
Subtotal: 80.0
Discount(0%): -0.0
Total Amount: 80.0
---------------------------------------------
```

## License

This project is open-source and available under the MIT License.
