# Code-Tech-task-4-internship- 
name: Paeimala madanapalle 

CodTech Internship Task 4: Advanced Encryption Tool

""" This is a simple AES-256-based file encryption and decryption tool using Python's 'cryptography' module. """

import os from cryptography.fernet import Fernet

Function to generate and save a key

def generate_key(): key = Fernet.generate_key() with open("secret.key", "wb") as key_file: key_file.write(key) print("[+] Key generated and saved to 'secret.key'")

Function to load the key from file

def load_key(): return open("secret.key", "rb").read()

Function to encrypt a file

def encrypt_file(filename, key): f = Fernet(key) with open(filename, "rb") as file: file_data = file.read() encrypted_data = f.encrypt(file_data) with open(filename + ".enc", "wb") as file: file.write(encrypted_data) print(f"[+] Encrypted: {filename} → {filename}.enc")

Function to decrypt a file

def decrypt_file(filename, key): f = Fernet(key) with open(filename, "rb") as file: encrypted_data = file.read() decrypted_data = f.decrypt(encrypted_data) original_filename = filename.replace(".enc", "_decrypted") with open(original_filename, "wb") as file: file.write(decrypted_data) print(f"[+] Decrypted: {filename} → {original_filename}")

User Interface

def main(): print("CodTech Internship Task 4 - Advanced Encryption Tool") print("1. Generate Key") print("2. Encrypt File") print("3. Decrypt File") choice = input("Enter choice (1-3): ")

if choice == "1":
    generate_key()
elif choice in ["2", "3"]:
    if not os.path.exists("secret.key"):
        print("[-] Key not found. Generate it first.")
        return
    key = load_key()
    filename = input("Enter the file path: ")
    if not os.path.exists(filename):
        print("[-] File not found.")
        return
    if choice == "2":
        encrypt_file(filename, key)
    else:
        decrypt_file(filename, key)
else:
    print("[-] Invalid choice")

if name == "main": main()

