# Finale-Project
Cone Control GUI

import tkinter as tk
from tkinter import messagebox

# prices and items
ice_creams = {
    "Vanilla": 79.99,
    "Chocolate": 79.99,
    "Strawberry": 81.99,
    "Mint Chocolate Chip": 81.99,
    "Cookies and Cream": 79.99
}

toppings = {
    "Hot Fudge": 30.99,
    "Sprinkles": 46.49,
    "Crushed Nuts": 63.49,
    "Whipped Cream": 78.49,
    "Caramel Sauce": 148.99
}

cones = {
    "Waffle Cones": 41.99,
    "Wafer Cones": 58.49
}

sales_tax_rate = 0.07 # 7% sales tax

def show_items(item_dict):
    return "\n".join([f"{name}: ${price:.2f}" for name, price in item_dict.items()])

def calculate_total(order_items):
    total = sum(price * quantity for price, quantity in order_items)
    sales_tax = total * sales_tax_rate
    return total, sales_tax

def order_summary():
    order_items = []
    for entry in entries:
        if entry[1].get().isdigit() and entry[0].get() in item_price_dict:
            quantity = int(entry[1].get())
            price = item_price_dict[entry[0].get()]
            order_items.append((price, quantity))
    
    total, sales_tax = calculate_total(order_items)
    total_with_tax = total + sales_tax

    messagebox.showinfo("order summary", f"Total: ${total:.2f}\nSales Tax: ${sales_tax:.2f}\nTotal with Tax: ${total_with_tax:.2f}")

# GUI setup
root = tk.Tk()
root.title("Cone Control")

item_price_dict = {**ice_creams, **toppings, **cones}
entries = []

# item list buttons
def show_ice_creams():
    messagebox.showinfo("Ice Cream Flavors", show_items(ice_creams))

def show_toppings():
    messagebox.showinfo("Toppings", show_items(toppings))

def show_cones():
    messagebox.showinfo("Cone Options", show_items(cones))

# buttons for viewing items
btn_ice_creams = tk.Button(root, text="Show Ice Cream Flavors", command=show_ice_creams)
btn_ice_creams.pack(pady=5)

btn_toppings = tk.Button(root, text="Show Toppings", command=show_toppings)
btn_toppings.pack(pady=5)

btn_cones = tk.Button(root, text="Show Cone Options", command=show_cones)
btn_cones.pack(pady=5)

# input fields for ordering
tk.Label(root, text="Enter your order (item: quantity)").pack(pady=10)

for item in item_price_dict.keys():
    frame = tk.Frame(root)
    frame.pack(pady=2)

    item_var = tk.StringVar(value=item)
    quantity_var = tk.StringVar(value="0")

    entry_item = tk.Entry(frame, textvariable=item_var, width=20, state='readonly')
    entry_quantity = tk.Entry(frame, textvariable=quantity_var, width=5)

    entry_item.pack(side=tk.LEFT)
    entry_quantity.pack(side=tk.LEFT)

    entries.append((item_var, quantity_var))

# button to calculate total
btn_order = tk.Button(root, text="Calculate Total", command=order_summary)
btn_order.pack(pady=20)

root.mainloop()
