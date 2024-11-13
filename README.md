# Password-Manager
### Table of content
- Project Overview
- Installation and Setup
- SubtleCrypto API

### Project Overview
This is a simple secure password manager using Node.js, Express, and the SubtleCrypto API, which allows users to securely store, retrieve, and manage their passwords through various endpoints. The server uses AES-GCM encryption for secure data storage and retrieval, ensuring that passwords are protected at all times.

A keychain is implemented in password-manager.js and provides methods for initializing, loading, setting, getting, and removing entries. Keychain data is encrypted using AES-GCM, and keys are derived using PBKDF2 with a random salt.

## Installation and Setup
1. Clone the Repository
https://github.com/FirdawsM/Password-Manager.git

cd Password-Manager-main

3.	Install Dependencies
npm install

4.	Run the Server
node manage/server.js

5.	Access the Application
Open your browser and go to http://localhost:3000

### SubtleCrypto API
- GET /: Serves the index.html file.
- POST /init: Initializes a new keychain with a given password.
 - Request body: { "password": "your_password" }
 - Response: { "message": "Keychain initialized", "data": < keychain-data> }
-POST /load: Loads an existing keychain from keychain.json using a given password.
 - Request body: { "password": "your_password" }
 - Response: { "message": "Keychain loaded", "keychain": < keychain-data > }
-POST /set: Sets a new entry in the keychain.
 - Request body: { "name": "entry_name", "value": "entry_value" }
 - Response: { "message": "Entry set" }
- GET /get/: Retrieves an entry from the keychain.
  - Response: { "value": "entry_value" }
- POST /remove: Removes an entry from the keychain.
 - Request body: { "name": "entry_name" }
 - Response: { "message": "Entry removed" }
- GET /dump: Dumps the entire keychain.
  - Response: { "repr": < keychain-data > }


### Key Processes
1.	Initializing the Keychain: Creates a new keychain with a password that will be used to derive a cryptographic key for encryption.
    - Process:
    A random salt is generated.
    The password is used along with the salt to derive an encryption key using the PBKDF2 algorithm.
    An empty keychain is created and stored in memory.
    The keychain data (including the salt) is saved to a file (keychain.json).
2.	Loading an Existing Keychain: Loads an existing keychain from a file using a password.
    - Process:
    The keychain data is read from the file.
    The password and salt are used to derive the decryption key.
    The encrypted keychain data is decrypted using the derived key.
    The keychain is restored in memory.
3.	Setting an Entry in the Keychain: Stores a new password or secret in the keychain.
	- Process:
    The value (e.g., password) is encrypted using the key derived from the user's password.
    The encrypted value is stored in the keychain with the provided name as the key.
4.	Getting an Entry from the Keychain: Retrieve a stored password or secret from the keychain.
	- Process:
    The encrypted value is fetched from the keychain using the provided name.
    The value is decrypted using the derived key.
    The decrypted value is returned to the user.
5.	Removing an Entry from the Keychain: Delete a stored password or secret from the keychain.
	- Process: The entry is removed from the keychain data structure.
6.	Dumping the Keychain: Export the entire keychain data in an encrypted form.
	- Process:
	The keychain data is encrypted using the derived key.
	The encrypted data, along with the salt, is returned or saved to a file.
