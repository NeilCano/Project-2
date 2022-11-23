# Project-2
#prueba N2
import datetime

class Abc:
    profiles=[[]] #for storing profiles details
    
    def signUp(self):
        name=input("Please enter your name : ")
        ph=input("Please enter your mobile number : ")
        pwd=input("Please enter your Password : ")
        con_Pwd=input("Please confirm your Password : ")
        dob=input("please Enter your Date of Birth # DD/MM/YY (No Space) : ")
        #check phone numbner is correct
        if(ph[0]!=0 and len(ph)!=10): 
            print("You have enter Phone number invalid format")
            print("Please try again:")
            return False
        #check password last digit is numric
        if( pwd[-1].isnumeric()==False):
            print("Password should end with number")
            print("Please try again:")
            return False
        #check these charactors are present in password
        character=['@','#','$']
        result = [ele for ele in character if(ele in pwd)] #return false if this charactore not present
        if(result==False):
            print("Password should include @,# or $")
            print("Please try again:")
            return False

        #check password and confirm password is not correct
        if(pwd!=con_Pwd):
            print("Your password should be same")
            print("Please try again:")
            return False

       #checking date format
        out=True
        try:
            day, month, year = dob.split('/') #split the date, month and year
            datetime.datetime(int(year), int(month), int(day))  #check its in date format
        except ValueError:
            out = False #if not return false
        if(out==False):
            print("Date should be in correct format")
            print("Please try again:")
            return False
        
        #check age
        dob_year=dob[-3:]  #return last 4 letters of dob, (year of birth)
        if((2022-int(dob_year))<18):
            print("Your age should be atleast 18 year old")
            print("Please try again:")
            return False

        #create a list with the details
        lst=[name,ph,pwd,con_Pwd,dob]  #append this list to the profiles list
        self.profiles.append(lst)
        print("You have sussesfully signed up")


    def Login(profiles):
        login_attempt=0 #to count invalid login attempt
        while(True):
            uname=input("Please enter your username (mobile numbner) ")
            pwd= input("Please enter your password ")

            login_flag=False  #flag for sucess login
            for list in profiles:  #list is each list in profiles(multiimentional list)
                for i in range(0,len(list)):  #iterate through the list elements
                    if(list[1]==uname and list[2]==pwd):  #check uname and pwd is in the list at the correct pos
                        login_flag=True 
                        name=list[0]  #name is stored to name

            if(login_flag==False):  #if login is false invalid_attempt increase
                print("You are not authorised")
                login_attempt=login_attempt+1
            
            else:
            #sucess login
                print("You have successfully signed in ")
                print("welecome "+name)
            #break from entire loop
#     #give more options
# while(True):
#         print("Please enter 1 for resetting the password :")
#         print("Please enter 2 for signout")
#         choice=input()
#         #if choice is 1 . reset() from task3 is called
#         if(choice=="1"):
#             reset(profiles)
#         if(choice=="2"):
#             print("you have sucessfuly logged out")
#             break
# #main body

while(True):
    print("Please enter 1 for signup:")
    print("Please enter 2 for login:")
    print("Please enter 3 for exit:")
    choice=input()
    #if choice is 1 new class objeect is created for Abc is created anbd signUp function is called
    if(choice=="1"): 
        o=Abc()
        o.signUp()

    #if choice is 2 login method from task2 file is called passing the profile list
    if(choice=="2"):
        o=Abc()
        o.Login()

    #if choice is 3 break from loops
    if(choice=="3"):
        print("Thank you for using the application")
        break
    if(choice == "2.1"):
        break
       
def login2():
    while (True): 
        print("Please enter 1 for signup: ")
        print("Please enter 2 for login: ")
        print("Please enter 3 for exit: ")
        choice1=input()
        
        if(choice1 == "2.1"):
            print()
            #self.dineIn
                
        if(choice1 == "2.2"):
            print("you are in statistics")

        if(choice1 == "2.3"):
            print("Thank you for using the application")
            break
