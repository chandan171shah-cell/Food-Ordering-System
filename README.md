# Food-Ordering-System
import pymongo as py
Client=py.MongoClient("mongodb://localhost:27017/")
database=Client["Project"]
Collection=database["users"]

def menuitems(Phone,Name):
    
            print("Welcome ",Name)
            menuItem=["Pizza","Burger","Chowmin","Momos","SpringRoll"]
            Price=[120,20,50,50,50]
        
            for i,j in enumerate(menuItem):
                 a=i+1   
                 print(a,"Item is ",j,"Price is",Price[i] )
            
            item1=0
            item2=0
            item3=0
            item4=0
            item5=0
        
            itemquantity1=0
            itemquantity2=0
            itemquantity3=0
            itemquantity4=0
            itemquantity5=0
            i=1
            while(i==1):
                Choicemenu=int(input("Enter Your Choice Which You Want to order"))
                match Choicemenu:
            
                    case 1:
                        item1=1
                        print("Pizza is Selected")
                        itemquantity1=int(input("Enter your quantity which you want to order"))
                    case 2:
                        item2=1
                        print("Burger is Selected")
                        itemquantity2=int(input("Enter your quantity which you want to order"))
                    case 3:
                        item3=1
                        print("Chowmin is Selected")
                        itemquantity3=int(input("Enter your quantity which you want to order"))
                    case 4:
                        item4=1
                        print("Momos is Selected")
                        itemquantity4=int(input("Enter your quantity which you want to order"))
                    case 5:
                        item5=1
                        print("Spring Roll is Selected")
                        itemquantity5=int(input("Enter your quantity which you want to order"))
    
                i=int(input("press 1: for more else press any key"))
            menutotal=0
            orderarr=[]
            if(item1==1):
                itemtotal=itemquantity1*Price[0]
                print("Your Item is",menuItem[0],"Your Price is ",Price[0],"and quantity is ",itemquantity1, "total is :-",itemtotal)
                menutotal=itemtotal+menutotal
                obj1={
                    "Item":menuItem[0],
                    "Price":Price[0],
                    "Quantity":itemquantity1,
                    "itemTotal":itemtotal
                } 
                orderarr.append(obj1)
            if(item2==1):
                itemtotal=itemquantity2*Price[1]
                print("Your Item is",menuItem[1],"Your Price is ",Price[1],"and quantity is ",itemquantity2, "total is :-",itemtotal)
                menutotal=itemtotal+menutotal
                obj2={
                    "Item":menuItem[1],
                    "Price":Price[1],
                    "Quantity":itemquantity2,
                    "itemTotal":itemtotal
                } 
                orderarr.append(obj2)
            if(item3==1):
                itemtotal=itemquantity3*Price[2]
                print("Your Item is",menuItem[2],"Your Price is ",Price[2],"and quantity is ",itemquantity3, "total is :-",itemtotal)
                menutotal=itemtotal+menutotal
                obj3={
                    "Item":menuItem[2],
                    "Price":Price[2],
                    "Quantity":itemquantity3,
                    "itemTotal":itemtotal
                } 
                orderarr.append(obj3)
            if(item4==1):
                itemtotal=itemquantity4*Price[3]
                print("Your Item is",menuItem[3],"Your Price is ",Price[3],"and quantity is ",itemquantity4, "total is :-",itemtotal)
                menutotal=itemtotal+menutotal
                obj4={
                    "Item":menuItem[3],
                    "Price":Price[3],
                    "Quantity":itemquantity4,
                    "itemTotal":itemtotal
                } 
                orderarr.append(obj4)
            if(item5==1):
                itemtotal=itemquantity5*Price[4]
                print("Your Item is",menuItem[4],"Your Price is ",Price[4],"and quantity is ",itemquantity5, "total is :-",itemtotal)
                menutotal=itemtotal+menutotal
                obj5={
                    "Item":menuItem[4],
                    "Price":Price[4],
                    "Quantity":itemquantity5,
                    "itemTotal":itemtotal
                } 
                orderarr.append(obj5)
            
            main={
                "Orders":orderarr,
                "userPhone":Phone,
                "Bill":menutotal
            }
            database["orders"].insert_one(main)
            print("total price is :-",menutotal)
    
print("Press 1: for New Customer")
print("Press 2: for Existing Customer")
choice= int(input("Enter Your Choice"))

match choice:

    case 1:
        Name=input("Enter Your Name")
        Phone=input("Enter Your Phone")
        Email=input("Enter Your Email")
        Address=input("Enter Your Address")

        obj={
            "Name":Name,
            "Phone":Phone,
            "Email":Email,
            "Address":Address
        }
        result=Collection.find_one({"Phone":Phone})
        if(result==None):
            result=Collection.insert_one(obj)  
            menuitems(Phone,Name)
        else:
            print("user already Exist")
    case 2:
        Phone=input("Enter Your Phone")
        result=Collection.find_one({"Phone":Phone})
        if(result==None):
            print("User Not Found")      
        else:
            name=result["Name"]
            menuitems(Phone,name)
