class Contact:
    def __init__(self, name, phone, email):
        self.name = name
        self.phone = phone
        self.email = email

    def display(self, index):
        print(f"|   {index:<4} | {self.name:<15} | {self.phone:<12} | {self.email:<20} |")

def print_header():
    print("\n" + "═" * 70)
    print("             📇 CONTACT DIRECTORY")
    print("═" * 70)
    print("|  S.No  |      Name       |   Phone No   |       Email            |")
    print("|--------|-----------------|--------------|------------------------|")

def main():
    contacts = []
    
    while True:
        print_header()
        for idx, contact in enumerate(contacts, start=1):
            contact.display(idx)

        print("═" * 70)
        print("Options:")
        print("[1] Add New Contact   [2] Search Contact")
        print("[3] Delete Contact    [4] Exit")
        print("═" * 70)
        try:
            choice = int(input("Enter your choice: "))
        except ValueError:
            print("⚠ Invalid input. Please enter a number.")
            continue

        if choice == 1:
            name = input("Enter Name: ")
            phone = input("Enter Phone: ")
            email = input("Enter Email: ")
            contacts.append(Contact(name, phone, email))
            print("✅ Contact added successfully!")

        elif choice == 2:
            search_name = input("Enter name to search: ").lower()
            found = False
            for idx, contact in enumerate(contacts, start=1):
                if search_name in contact.name.lower():
                    print("🔍 Contact Found:")
                    contact.display(idx)
                    found = True
            if not found:
                print("❌ No contact found with that name.")

        elif choice == 3:
            try:
                del_index = int(input("Enter contact number (S.No) to delete: "))
                if 1 <= del_index <= len(contacts):
                    to_delete = contacts[del_index - 1]
                    print("Are you sure you want to delete this contact?")
                    to_delete.display(del_index)
                    confirm = input("Type 'yes' to confirm: ").lower()
                    if confirm == 'yes':
                        contacts.pop(del_index - 1)
                        print("🗑 Contact deleted successfully!")
                    else:
                        print("❌ Deletion cancelled.")
                else:
                    print("❌ Invalid contact number.")
            except ValueError:
                print("⚠ Please enter a valid number.")

        elif choice == 4:
            print("👋 Exiting... Thank you for using Contact Directory!")
            break

        else:
            print("⚠ Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
