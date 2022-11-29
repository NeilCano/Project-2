from datetime import datetime, date
import sys 

class User(): 
    username = ''
    password = ''
    address = ''
    mobile =0
    dateBirth= datetime.now()
    age=0

class OrderAvailable(object):
    amount = 0
    date = datetime.now()
    id = 0
    def __init__(self, products, type):
        self.products = products
        self.type = type
    

class ProductsAvailable(object):
    def __init__(self, name, price):
        self.name = name
        self.price = price

def password_check(passwd):
    SpecialSym =['$', '@', '#', '%']
    val = True
    if not any(char.isdigit() for char in passwd):
        print('Password should have at least one numeral')
        val = False
    if not any(char in SpecialSym for char in passwd):
        print('Password should have at least one of the symbols $@#')
        val = False
    if val:
        return val

def age(birthdate):
    today = date.today()
    age = today.year - birthdate.year - ((today.month, today.day) < (birthdate.month, birthdate.day))
    return age

def SignUp(user):
    user.name = input('Please enter your name:')
    user.address = input('Please enter your address or press enter to skip:')
    while True:
        user.mobile = input("Please enter your mobile number:")
        if len(user.mobile) != 10 or int(str(user.mobile)[:1]) != 0:
            print("The mobile number has 10 digits and must starts with 0 .")
        else:
            break

    while True:
        user.password = input("Please enter your password:")
        if not password_check(user.password):
            print("Invalid Password !!1")
        else:
            break

    while True:
        user.password = input("Please re- enter your password:")
        if not password_check(user.password):
            print("Invalid Password !!")
        else:
            break

    while True:
        user.dateBirth = input("Please enter your Date of Birth # DD/MM/YYYY (No Space):")
        try:
            user.dateBirth = datetime.strptime(user.dateBirth, '%d/%m/%Y')
            user.age = int(age(user.dateBirth))
            if  user.age<18:
                print("Invalid Age !!")
            else:
                break
        except ValueError:
            print()
    
    print("You have successfully signed up")


def Ordering(order):
    print(" Please Enter 1 to for Dine in \n Please enter 2 for Order Online \n Please enter 3 to go Login Page ")
    menu = int(input())
    if menu==1:
        Order(order, 'DineIn')
    elif menu==2:
        Order(order, 'OrderOnline')
    else:
        sys.exit()


def Order(order, type):
    productsAvailable = []
    productsAvailable.append(ProductsAvailable('Noodles',2))
    productsAvailable.append(ProductsAvailable('Sandiwch',4))
    productsAvailable.append(ProductsAvailable('Dumpling',6))
    productsAvailable.append(ProductsAvailable('Muffins',8))
    productsAvailable.append(ProductsAvailable('Pasta',10))
    productsAvailable.append(ProductsAvailable('Pizza',20))

    while True:
        print(" Enter 1 for Noodles Price AUD 2 \n Enter 2 for Sandiwch Price AUD 4 \n Enter 3 for Dumpling AUD 6 \n Enter 4 for Muffins Price AUD 8 \n Enter 5 for Pasta Price AUD 10 \n Enter 6 for Pizza Price AUD 20 \n Enter 7 for Drinks Menu: ")
        menu = int(input())
        if menu <= 6:
            order.append(productsAvailable[menu-1])
        elif menu == 7:
             OrderDrinks(order, type)
             break;
        else:
            break

def OrderDrinks(order, type):
    while True:
        print("Enter 1 for Coffee Price AUD 2 \n  Enter 2 for Colddrink Price AUD 4 \n  Enter 3 for Shake AUD 6 \n   Enter 4 for checkout ")
        menu = int(input())
        if menu == 1:
            product = ProductsAvailable('Coffee', 2)
            order.append(product)
        elif menu == 2:
            product = ProductsAvailable('Colddrink', 2)
            order.append(product)
        elif menu == 3:
            product = ProductsAvailable('Shake', 6)
            order.append(product)
        elif menu == 4:
            Checkout(order, type)
            break;
        else:
            break


def Checkout(order, type):
    orderFinally = OrderAvailable(order, type)
    price = 0
    for product in orderFinally.products:
        price += product.price

    serviceCharges=0
    if orderFinally.type == 'DineIn':
        serviceCharges += (15 * price) / 100.0

    print("Your total payble amount is: " + str(price) + " inclusing AUD " + str(serviceCharges) + " for Service Charges, please click  'yes' for Collect or  'no' for cancel the order")
    menu = input()
    if menu == 'yes':
        print("A fix charges for Delivery based on the distance i.e.\n More than 0 to 5 Kms AUD 5 \n More than 5 to 10 Kms AUD 10 \n More than 10 to 15 Kms AUD 18 \n More than 15Kms No Delivery provided")
        menu = int(input())
        if menu == 1:
            serviceCharges += 5
        elif menu == 2:
            serviceCharges += 10
        elif menu == 3:
            serviceCharges += 12
        elif menu == 4:
            serviceCharges += 0
    elif menu == 'no':
        SignIn()
    else:
        sys.exit()
    
    price += serviceCharges
    print("Your total payble amount is: " + str(price) + "inclusing AUD " + str(serviceCharges) + "for additional charges for delivery")
    print("please click  'yes' to confirm the order, or 'no' to cancel")
    

    menu = input()
    if menu == 'yes':
        orderFinally.amount = price
        orderFinally.id = len(orders) + 1
        orders.append(orderFinally)
        print("Thank you for the confirmation, your order has been confirmed")
        Menu([])
    elif menu == 'no':
        SignIn(orderFinally)

def History():
    print("Please Enter the option to Print the Statistics \n 1 - All Dine in Orders  \n 2 - All Pick up Orders \n 3 - All Deliveries \n 4 - Total Amount Spent on All Orders  ")
    menu = int(input())
    if menu == 1:
        print(f'Date    |Order Id   |Type of Order  |Order Amount   ')
        for order in orders:
            if order.type == 'DineIn':
                print(f'{str(order.date)}   |{str(order.id)}    |{str(order.type)}  |{str(order.amount)}')
    elif  menu == 2:
        print(f'Date    |Order Id   |Type of Order  |Order Amount   ')
        for order in orders:
            if order.type == 'OrderOnline':
                print(f'{str(order.date)}   |{str(order.id)}    |{str(order.type)}  |{str(order.amount)}')
    elif menu == 3 :
        print(f'Date    |Order Id   |Type of Order  |Order Amount   ')
        for order in orders:
            print(f'{str(order.date)}   |{str(order.id)}    |{str(order.type)}  |{str(order.amount)}')
    elif menu == 4:
        totalAmount = 0
        for order in orders:
            totalAmount += order.amount
        print(f'Total Amount Orders :{str(totalAmount)}')
    Menu([])
def SignIn():
    user.username = input("Please enter your Username(Mobile Number):")
    user.password = input("Please enter your password:")
    order = []
    Menu(order)

def Menu(order):
    print("You have successfully Signed In  \n Please Enter 1 to start Ordering  \n Please enter 2 to print statics \n Please Enter 3 for Logout  ")
    menu = int(input())
    if menu==1:
        Ordering(order)
    elif menu==2:
        History()
    else:
        sys.exit()

def Quit():
  print("Hello!")

user = User()
menu = 0
orders = []
print("Please Enter 1 for Sign up.  \nPlease Enter 2 for Sign in  \nPlease Enter 3 for Quit. ")
menu = int(input())
if menu==1:
    SignUp(user)
elif menu==2:
    SignIn()
else:
    sys.exit()

