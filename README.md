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
