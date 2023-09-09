import mysql.connector as c
con=c.connect(host='localhost',user='root',database='devops',passwd='passkey=00')
cursor=con.cursor()
def add_password(username, password,website):
    cursor.execute("INSERT INTO password (Username, Password,website) VALUES ({},{},{})".format(username,password,website))
    con.commit()
def table():
    cursor.execute("SELECT Username,website from password")
    r=cursor.fetchall()
    if r:
        print("____________________")
        print("[Username , Website ]")
        for i in r:
            L=list(i)
            print(L)
    else:
        print("No saved password")
        return -1
    print("      ")
def get_password(username):
    cursor.execute("SELECT Password FROM Password where Username = {}".format(username))
    result = cursor.fetchone()
    if result:
        return result[0]
    else:
        return None
def main():
    print("_______Password Manager________")
    print("----------------------------------------------")
    while True:
        print("\nOptions:")
        print("1. Add Password")
        print("2. Get Password")
        print("3. Exit")
        choice = input("Enter your choice: ")
        if choice == '1':
            username = input("Enter username: ")
            password = input("Enter password: ")
            website = input("Enter website name: ")
            add_password(username, password,website)
            print("Password added Successfully!")
        elif choice == '2':
            a=table()
             if a!=-1:
                 username = input("Enter username: ")
                 password = get_password(username)
                 if password:
                     print(f"Password for {username}: {password}")
                 else:
                     print(f"No password found for {username}")
        elif choice == '3':
            break
        else:
            print("Please select a valid option.")
            continue
    print("Goodbye!")
main()

