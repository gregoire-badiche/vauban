# Vauban

A secure hardware password vault and authentication device for maximum password integrity

![Display for Vauban](https://github.com/gregoire-badiche/vauban/blob/main/docs/images/VAUBAN.png "Affiche Vauban")

## What is Vauban?

In today’s digital landscape, strong authentication is more critical than ever. Vauban is a hardware-based password vault and authentication device designed to keep your passwords safe from online servers and vulnerable computers. By combining multiple authentication factors, it ensures that only you can access your accounts and data. With its USB interface, Vauban can instantly enter authentication secrets for you on any machine, streamlining your login experience.

### Why multiple authentication factors matter

Effective identity verification relies on a combination of distinct factors, often categorized into three groups:

- **Something you know**  
   Information unique to you, such as passwords, PINs, or secret phrases. These knowledge-based factors are fundamental but can be compromised without additional security layers.  

- **Something you are**  
   Biometrics like your fingerprint, iris, or voice. These are unique to you and challenging to replicate, adding a strong layer of identity verification.  

- **Something you have**  
   Physical objects like a hardware token, smart card, or, in Vauban’s case, a secure device. These require physical possession, providing a critical safeguard that passwords or biometrics alone cannot.  

### What does Vauban do?

Vauban integrates these authentication factors to deliver comprehensive security, focusing on property-based protection (the “something you have” factor). Here’s how it works:

- **Secure password storage:**  
   All credentials are encrypted and stored locally on the device, never on a server, ensuring your data stays under your control.  

- **Simplified access:**  
   Vauban manages multiple passwords for you, allowing each to meet stringent security requirements, such as including unusual characters. Vauban types these passwords for you, so you don’t have to remember them.  

- **Enhanced security:**  
   Acting as a hardware authentication device, Vauban strengthens account protection with multi-factor authentication (MFA). For example, it pairs property-based security (something you have) with biometrics or a passphrase to unlock the database.  

### What doesn't Vauban do?

While Vauban offers robust protection, it’s important to understand its limitations:

- **Vulnerability to physical theft:**  
   As a property-based security system, Vauban is vulnerable if stolen.  

- **Susceptibility to keyloggers:**  
   Vauban signals itself as a keyboard to input passwords. This approach means it could be compromised by keyloggers on the host system.  

- **No wireless connectivity:**  
   Although the chip has built-in Bluetooth and WiFi capabilities, Vauban lacks antennas for these technologies, ensuring it cannot connect to wireless networks.  

- **Potential NFC interception:**  
   Vauban decrypts its database using authentication information from your phone via NFC. While convenient, these signals could potentially be intercepted.  

## How does it work?

Vauban encrypts your passwords and authentication information in a database similar to KeePass (though less customizable). It sends this data via USB using the HID protocol, functioning like a keyboard.

You can decrypt the database using:  

- A **master password** you provide,  
- A password sent by your phone over NFC (which requires your phone to be unlocked using its PIN or fingerprint), or  
- The built-in **fingerprint reader** on Vauban.  

The device uses two SPI chips to store the database, with one serving as a backup. The database specs can be found in the `docs` folder.

Huge thanks to Keepass for inspiring this project and the database organisation and cryptic security.
