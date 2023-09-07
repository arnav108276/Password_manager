import mysql.connector as co
con=co.connect(host='localhost',user='root',database='devops',passwd='passkey=00')
cursor=con.cursor()
def add_password(username, password):
    cursor.execute("INSERT INTO password (Username, Password) VALUES ({},{})".format(username,password))
    con.commit()
def get_password(username):
    cursor.execute("SELECT password FROM Password WHERE Username = {}".format(username))
    result = cursor.fetchone()
    if result:
        return result[0]
    else:
        return None
def main():
    print("_______Password Manager________")
    print("--------------------")
    while True:
        print("\nOptions:")
        print("1. Add Password")
        print("2. Get Password")
        print("3. Exit")
        choice = input("Enter your choice: ")
        if choice == '1':
            username = input("Enter username: ")
            password = input("Enter password: ")
            add_password(username, password)
            print("Password added successfully!")
        elif choice == '2':
            username = input("Enter username: ")
            password = get_password(username)
            if password:
                print(f"Password for {username}: {password}")
            else:
                print(f"No password found for {username}")
        elif choice == '3':
            break
        else:
            print("Invalid choice. Please select a valid option.")
    print("Goodbye!")
main()

