# banking-sysytem
banking repositry
from tkinter import *
from tkinter import font
import mysql.connector as sqlc
from PIL import ImageTk,Image


#database

db=sqlc.connect(
    host="localhost",
    username="root",
    password="S@njay123",
    database="database_2"
   )

cursor=db.cursor()

#table="""CREATE TABLE Banksys
#    (
#        Name VARCHAR(255),
#        Age int,
#        Gender VARCHAR(255),
#        Password VARCHAR(255),
#        Balance int DEFAULT 0
#    );"""

#cursor.execute(table)


db.commit()
db.close()

def w_finish():


    db=sqlc.connect(
        host="localhost",
        username="root",
        password="S@njay123",
        database="database_2"
         )

    cursor=db.cursor()
    cursor.execute('select * from banksys where Name=%s and Password=%s',(name,password))
    w_row=cursor.fetchone()

    if w_e1.get()=="" or float(w_e1.get())<=0 or float(w_e1.get())>w_row[4]:
        notif_w.config(fg="red",text="Please fill the Amount correctly")
    

    
    else:
        

        current_balance=w_row[4]
        updated_balance=current_balance
        updated_balance=updated_balance - float(w_e1.get())

        
    
        cursor.execute("UPDATE banksys SET Balance=%s WHERE Name=%s and Password=%s",(updated_balance,name,password))

        w_l3.config(text="$"+str(updated_balance))

        notif_w.config(fg="green",text="Updated successfully")
        w_e1.delete(0,END)
        



        db.commit()

        db.close()
    

def d_finish():

    if d_e1.get()=="" or float(d_e1.get())<=0:
        notif_d.config(fg="red",text="Please fill the Amount correctly")

    
    else:
        db=sqlc.connect(
        host="localhost",
        username="root",
        password="S@njay123",
        database="database_2"
         )

        cursor=db.cursor()
        cursor.execute('select * from banksys where Name=%s and Password=%s',(name,password))
        d_row=cursor.fetchone()

        current_balance=d_row[4]
        updated_balance=current_balance
        updated_balance=updated_balance + float(d_e1.get())

        
    
        cursor.execute("UPDATE banksys SET Balance=%s WHERE Name=%s and Password=%s",(updated_balance,name,password))

        d_l3.config(text="$"+str(updated_balance))

        notif_d.config(fg="green",text="Updated successfully")
        d_e1.delete(0,END)
        



        db.commit()

        db.close()
    

       

        
        

    
            
    


def deposit():
    global deposit_screen
    global d_e1
    global d_l3
    global notif_d

    deposit_screen=Toplevel()
    deposit_screen.title("Deposit Money")
    frame5=LabelFrame(deposit_screen,text="Deposit Money",padx=50,pady=50)
    frame5.pack(padx=50,pady=50)

    d_l1=Label(frame5,text="Deposit",font=("New Times Roman",16,"bold"),fg="#0C0C0B")
    d_l1.grid(row=0,column=0,columnspan=2)

    d_l2=Label(frame5,text="Current Balance:",font=("New Times Roman",14),fg="#0C0C0B")
    d_l2.grid(row=1,column=0)

    db=sqlc.connect(
    host="localhost",
    username="root",
    password="S@njay123",
    database="database_2"
      )

    cursor=db.cursor()
    cursor.execute('select * from banksys where Name=%s and Password=%s',(name,password))
    bal=cursor.fetchone()

    d_l3=Label(frame5,text="$"+str(bal[4]),font=("New Times Roman",14),fg="#0C0C0B")
    d_l3.grid(row=1,column=1,sticky=W)

    db.commit()

    db.close()

    d_l2=Label(frame5,text="Amount:",font=("New Times Roman",14),fg="#0C0C0B")
    d_l2.grid(row=2,column=0,sticky=E)

    d_e1=Entry(frame5,width=15,bd=3)
    d_e1.grid(row=2,column=1,sticky=E)

    d_b1=Button(frame5,text="Finish",font=("Times New Roman",15),bg="#000000",fg="#FDFEFE",padx=7,command=d_finish)
    d_b1.grid(row=3,column=0,columnspan=2,padx=3,pady=5)

    notif_d=Label(frame5,font=("Times New Roman",14))
    notif_d.grid(row=4,pady=5)




    

def withdraw():
    global withdraw_screen
    global w_e1
    global w_l3
    global notif_w

    withdraw_screen=Toplevel()
    withdraw_screen.title("Deposit Money")
    frame6=LabelFrame(withdraw_screen,text="Withdraw Money",padx=50,pady=50)
    frame6.pack(padx=50,pady=50)

    w_l1=Label(frame6,text="Withdraw",font=("New Times Roman",16,"bold"),fg="#0C0C0B")
    w_l1.grid(row=0,column=0,columnspan=2)

    w_l2=Label(frame6,text="Current Balance:",font=("New Times Roman",14),fg="#0C0C0B")
    w_l2.grid(row=1,column=0)

    db=sqlc.connect(
    host="localhost",
    username="root",
    password="S@njay123",
    database="database_2"
      )

    cursor=db.cursor()
    cursor.execute('select * from banksys where Name=%s and Password=%s',(name,password))
    w_bal=cursor.fetchone()

    w_l3=Label(frame6,text="$"+str(w_bal[4]),font=("New Times Roman",14),fg="#0C0C0B")
    w_l3.grid(row=1,column=1,sticky=W)

    db.commit()

    db.close()

    w_l2=Label(frame6,text="Amount:",font=("New Times Roman",14),fg="#0C0C0B")
    w_l2.grid(row=2,column=0,sticky=E)

    w_e1=Entry(frame6,width=15,bd=3)
    w_e1.grid(row=2,column=1,sticky=E)

    w_b1=Button(frame6,text="Finish",font=("Times New Roman",15),bg="#000000",fg="#FDFEFE",padx=7,command=w_finish)
    w_b1.grid(row=3,column=0,columnspan=2,padx=3,pady=5)

    notif_w=Label(frame6,font=("Times New Roman",14))
    notif_w.grid(row=4,pady=5)





def personel():

    

    personel_screen=Toplevel()
    personel_screen.title("Personel Details")
    frame4=LabelFrame(personel_screen,text="Personel Details",padx=50,pady=50)
    frame4.pack(padx=50,pady=50)

    db=sqlc.connect(
    host="localhost",
    username="root",
    password="S@njay123",
    database="database_2"
      )

    cursor=db.cursor()
    cursor.execute('select * from banksys where Name=%s and Password=%s',(name,password))
    row=cursor.fetchone()

    

    l1=Label(frame4,text="Name:",font=("New Times Roman",16,"bold"),fg="#0C0C0B")
    l1.grid(row=0,column=0)
    l2=Label(frame4,text=row[0],font=("New Times Roman",16),fg="#0C0C0B")
    l2.grid(row=0,column=1)
    l3=Label(frame4,text="Age:",font=("New Times Roman",16,"bold"),fg="#0C0C0B")
    l3.grid(row=1,column=0)
    l4=Label(frame4,text=row[1],font=("New Times Roman",16),fg="#0C0C0B")
    l4.grid(row=1,column=1)
    l5=Label(frame4,text="Gender:",font=("New Times Roman",16,"bold"),fg="#0C0C0B")
    l5.grid(row=2,column=0)
    l6=Label(frame4,text=row[2],font=("New Times Roman",16),fg="#0C0C0B")
    l6.grid(row=2,column=1)
    l7=Label(frame4,text="Password:",font=("New Times Roman",16,"bold"),fg="#0C0C0B")
    l7.grid(row=3,column=0)
    l8=Label(frame4,text=row[3],font=("New Times Roman",16),fg="#0C0C0B")
    l8.grid(row=3,column=1)
    l9=Label(frame4,text="Balance:",font=("New Times Roman",16,"bold"),fg="#0C0C0B")
    l9.grid(row=4,column=0)
    l10=Label(frame4,text="$"+str(row[4]),font=("New Times Roman",16),fg="#0C0C0B")
    l10.grid(row=4,column=1)


    

    db.commit()

    db.close()


def login_session():
    global name
    global password
    if entry5.get()=="" or entry6.get()=="":
        notif1.config(fg="red",text="*All fields are required*")
    else:


        db=sqlc.connect(
        host="localhost",
        username="root",
        password="S@njay123",
        database="database_2"
        )

        cursor=db.cursor()
        
        
        cursor.execute('SELECT * from banksys where Name=%s and Password=%s',(entry5.get(),entry6.get()))
        detail=cursor.fetchone()
        if detail!=None:
            name=entry5.get()
            password=entry6.get()
            login_screen.destroy()
            account_dash=Toplevel()
            account_dash.title("Dashboard")
            frame3=LabelFrame(account_dash,text="*Home Page*",padx=50,pady=50)
            frame3.pack(padx=100,pady=100)
            
            #labels
            label10=Label(frame3,text="Account Dashboard",font=("New Times Roman",16,"bold"),fg="#0B3333")
            label10.grid(row=0,column=0,columnspan=2)
            label11=Label(frame3,text="Welcome "+ name,font=("New Times Roman",16,"bold"),fg="#331E0B")
            label11.grid(row=1,column=0,columnspan=2)

            #buttons
            button5=Button(frame3,text="Personel Details",font=("Times New Roman",15),bg="#000000",fg="#FDFEFE",padx=7,pady=3,command=personel)
            button5.grid(row=2,column=0,columnspan=2,pady=10)
            button6=Button(frame3,text="Deposit",font=("Times New Roman",15),bg="#000000",fg="#FDFEFE",padx=40,pady=3,command=deposit)
            button6.grid(row=3,column=0,columnspan=2,pady=10)
            button7=Button(frame3,text="Withdraw",font=("Times New Roman",15),bg="#000000",fg="#FDFEFE",padx=34,pady=3,command=withdraw)
            button7.grid(row=4,column=0,columnspan=2,pady=10)
        else:
            notif1.config(fg="red",text="credentials are incorrect!")





        db.commit()

        db.close()



def finish_reg():
    if entry1.get()=="" or entry2.get=="" or entry3.get()=="" or entry4.get=="":
        notif.config(fg="red",text="*All fields are required*")
        
    else:

        db=sqlc.connect(
         host="localhost",
         username="root",
         password="S@njay123",
         database="database_2"
         )

        cursor=db.cursor()
        
        cursor.execute("SELECT * FROM banksys")
        records=cursor.fetchall()
        print(records)
        if entry1.get()!="" and entry4.get()!="":
            count=0
            for x in records:
                if entry1.get()==x[0] and entry4.get()==x[3]:

                    notif.config(fg="blue",text="Account already exists!")
                    
                    count=1
                    break
                    
                
                
                
            print(count)
            if count!=1:      
                sql="INSERT INTO banksys (Name,Age,Gender,Password) VALUES (%s,%s,%s,%s)"  
                val=(entry1.get(),entry2.get(),entry3.get(),entry4.get())

                cursor.execute(sql,val)

                notif.config(fg="green",text="Registration done successfully!")

        db.commit()
        db.close()
                

    entry1.delete(0,END)
    entry2.delete(0,END)
    entry3.delete(0,END)
    entry4.delete(0,END)

def register():
    global register_screen
    global entry1
    global entry2
    global entry3
    global entry4
    global notif
    
    

    register_screen=Toplevel()
    register_screen.title("Register")
    frame1=LabelFrame(register_screen,text="Enter Your Details Below",padx=50,pady=50)
    frame1.pack(padx=100,pady=100)

    #labels
    label4=Label(frame1,text="Name:",font=("Times New Roman",14))
    label4.grid(row=0,column=0)
    label5=Label(frame1,text="Age:",font=("Times New Roman",14))
    label5.grid(row=1,column=0)
    label6=Label(frame1,text="Gender:",font=("Times New Roman",14))
    label6.grid(row=2,column=0)
    label7=Label(frame1,text="Password:",font=("Times New Roman",14))
    label7.grid(row=3,column=0)

    #notification
    notif=Label(frame1,font=("Times New Roman",14))
    notif.grid(row=5,pady=5)


    #entry
    entry1=Entry(frame1,width=15,bd=3)
    entry1.grid(row=0,column=1)
    entry2=Entry(frame1,width=15,bd=3)
    entry2.grid(row=1,column=1)
    entry3=Entry(frame1,width=15,bd=3)
    entry3.grid(row=2,column=1)
    entry4=Entry(frame1,width=15,bd=3,show="*")
    entry4.grid(row=3,column=1)

    


    button3=Button(frame1,text="Finish",font=("Times New Roman",15),bg="#000000",fg="#FDFEFE",padx=10,pady=3,command=finish_reg)
    button3.grid(row=4,column=0,columnspan=2,padx=20,pady=7)





def login():
    global login_screen
    global notif1
    global entry5
    global entry6


    login_screen=Toplevel()
    login_screen.title("login page")
    frame2=LabelFrame(login_screen,text="**LOGIN**",padx=50,pady=50)
    frame2.pack(padx=100,pady=100)

    #labels
    label8=Label(frame2,text="*Login to your Account*",font=("Times New Roman",14))
    label8.grid(row=0,column=0,columnspan=2,pady=5)
    label9=Label(frame2,text="UserName:",font=("Times New Roman",16,"bold"))
    label9.grid(row=1,column=0)
    label10=Label(frame2,text="Password:",font=("Times New Roman",16,"bold"))
    label10.grid(row=2,column=0)


    #notification
    notif1=Label(frame2,font=("Times New Roman",14))
    notif1.grid(row=4,pady=5)
    #entry
    entry5=Entry(frame2,width=15,bd=3)
    entry5.grid(row=1,column=1)
    entry6=Entry(frame2,width=15,bd=3,show="*")
    entry6.grid(row=2,column=1)

    button4=Button(frame2,text="Login",font=("Times New Roman",16),bg="#000000",fg="#FDFEFE",padx=15,pady=3,command=login_session)
    button4.grid(row=3,column=0,columnspan=2,pady=5)




root=Tk()
root.title("Banking App")

#import image
img_1=Image.open("images/bank3.jpg")
img_1=img_1.resize((180,160))
img_1=ImageTk.PhotoImage(img_1)

#labels
label1=Label(root,text="BANKING SYSTEM",font=("Times New Roman",16),fg="#555555")
label1.grid(row=0,padx=20,pady=10)
label2=Label(root,text="Your Own Secure Bank",font=("Times New Roman",16),fg="#555555")
label2.grid(row=1,padx=20,sticky=N)
label3=Label(root,image=img_1)
label3.grid(row=2,padx=17,pady=7)


#buttons
button1=Button(root,text="Register",font=("Times New Roman",18),bg="#000000",fg="#FDFEFE",padx=10,pady=3,command=register)
button1.grid(row=3,padx=20,pady=3)
button2=Button(root,text="Login",font=("Times New Roman",18),bg="#000000",fg="#FDFEFE",padx=22,pady=3,command=login)
button2.grid(row=4,padx=20,pady=3)






root.mainloop()
