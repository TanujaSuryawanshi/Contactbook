# Contactbook

import os

# File to store contacts
CONTACTS_FILE = 'contacts.txt'

# Load contacts from file
def load_contacts():
    contacts = []
    if os.path.exists(CONTACTS_FILE):
        with open(CONTACTS_FILE, 'r') as file:
            for line in file:
                name, phone, email = line.strip().split(',')
                contacts.append({'name': name, 'phone': phone, 'email': email})
    return contacts

# Save contacts to file
def save_contacts(contacts):
    with open(CONTACTS_FILE, 'w') as file:
        for contact in contacts:
            file.write(f"{contact['name']},{contact['phone']},{contact['email']}\n")

# Add new contact
def add_contact():
    name = input("Enter name: ")
    phone = input("Enter phone number: ")
    email = input("Enter email address: ")
    contacts = load_contacts()
    contacts.append({'name': name, 'phone': phone, 'email': email})
    save_contacts(contacts)
    print(f"Contact '{name}' added successfully!")

# View all contacts
def view_contacts():
    contacts = load_contacts()
    if contacts:
        print("\nContacts:")
        for contact in contacts:
            print(f"Name: {contact['name']}, Phone: {contact['phone']}, Email: {contact['email']}")
    else:
        print("No contacts found.")

# Search for a contact by name
def search_contact():
    name = input("Enter the name to search: ").lower()
    contacts = load_contacts()
    found = False
    for contact in contacts:
        if contact['name'].lower() == name:
            print(f"Name: {contact['name']}, Phone: {contact['phone']}, Email: {contact['email']}")
            found = True
    if not found:
        print(f"No contact found with the name '{name}'.")

# Delete a contact by name
def delete_contact():
    name = input("Enter the name to delete: ").lower()
    contacts = load_contacts()
    updated_contacts = [contact for contact in contacts if contact['name'].lower() != name]
    if len(contacts) == len(updated_contacts):
        print(f"No contact found with the name '{name}'.")
    else:
        save_contacts(updated_contacts)
        print(f"Contact '{name}' deleted successfully!")

# Main program loop
def main():
    while True:
        print("\n--- Contact Book ---")
        print("1. Add Contact")
        print("2. View Contacts")
        print("3. Search Contact")
        print("4. Delete Contact")
        print("5. Exit")

        choice = input("Enter your choice (1-5): ")

        if choice == '1':
            add_contact()
        elif choice == '2':
            view_contacts()
        elif choice == '3':
            search_contact()
        elif choice == '4':
            delete_contact()
        elif choice == '5':
            print("Exiting Contact Book.")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == '__main__':
    main()
