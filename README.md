Password Manager mini project

1. Discussion

I developed a password management system, using client-side encryption alongside JWT authentication.

On the client's side a Blazor WebAssembly was used, so the whole project runs on client's device, which makes it more secure compared to transmitting data from our server.

This has both pros and cons:

- Executing operations within a web browser leads to a decrease in performance, especially when it comes to cryptographic tasks. In our specific scenario, we found it necessary to lower the number of iterations to prevent the login page from experiencing excessive delays.
- We don't store the master password and it's also not transmitted to our servers


Upon login, the client's master password undergoes a PBKDF2 hashing process with their associated email, generating a Master Key. This key is pivotal for decrypting the vault.

Subsequently, the Master Key undergoes iterations of PBKDF2 hashing to produce the Master Hash. This hash serves as a substitute for a password when accessing the API.

During the login process, the API subjects the Master Hash to additional hashing via Argon2id, incorporating a random hash and pepper for secure storage within the database.

While the user is logged in, their master key is exclusively retained in memory. This implies that in the event of a connection loss or browser closure, the memory is wiped clean, rendering the master key inaccessible on the device (prompting the user to log in again).

When a new password is saved, both the email and password are encrypted using the Master Key before being stored in the database.

2.	Further suggestions
   
-	Stretching the master key to 512 bits
-	Rewrite the project and run it on our server, so it offers compability across multiple devices and user can login using their pc or mobile phone comfortably to access their data
-	Option to change password
-	Improve registration by adding "forgot password" option

  
3.	How to run

You need to start the Backend firstly, following by running the frontend. Open the 2 terminal windows in the project main folder and run following commands.
   
    a. Backend
  
        1. cd Pw_WebApi
        2. dotnet run
   
    a. Frontend
  
        1. cd PW_Frontend
        2. dotnet run
       

Matej Adamkovic

