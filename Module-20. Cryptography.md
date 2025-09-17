# Module 20

## Cryptography
Cryptography and cryptographic (“crypto”) systems help in securing data from interception and compromise during online transmissions. Cryptography enables one to secure transactions, communications, and other processes performed in the electronic world, and is additionally used to protect confidential data such as email messages, chat sessions, web transactions, personal data, corporate data, e-commerce applications, etc.

As an ethical hacker or penetration tester, you should suggest to your client proper encryption techniques to protect data, both in storage and during transmission. The labs in this module demonstrate the use of encryption to protect information systems in organizations.

---

### 1. Encrypt the Information using Various Cryptography Tools

#### 1.1 Calculate hash using hashcalc
[SlavaSoft Downloads](https://www.slavasoft.com/download.htm)

<img width="672" height="460" alt="image" src="https://github.com/user-attachments/assets/39fa891d-5e58-42dd-b687-3bd5c427aa57" />

#### 1.2 Calculate MD5 hashes using md5 calculator
[MD5 Calculator](https://md5calculator.com/)

<img width="634" height="455" alt="image" src="https://github.com/user-attachments/assets/8f61e666-4739-417e-a94c-f8fd0ef23764" />

#### 1.3 Calculate MD5 hashes using HashmyFiles
[HashMyFiles: Calculate MD5/SHA1/CRC32 hash of files](https://www.nirsoft.net/utils/hash_my_files.html)

<img width="629" height="245" alt="image" src="https://github.com/user-attachments/assets/25c31ac5-2af1-46a6-b4ae-a525483d6a20" />

#### 1.4 Perform File and Text Message  Encryption using cryptoforge
CryptoForge is a file encryption software for personal and professional data security. It allows you to protect the privacy of sensitive files, folders, or email messages by encrypting them with strong encryption algorithms. Once the information has been encrypted, it can be stored on insecure media or transmitted on an insecure network.

[Encryption Software | Data Encryption Software](https://www.cryptoforge.com/)

#### 1.5 Perform File encryption using Advanced encryption package
[File Encryption Software](https://www.aeppro.com/)

#### 1.6 Encrypt and Decrypt data using BCtextEncoder
[Encrypt Text with BCTextEncoder | Jetico](https://www.jetico.com/free-security-tools/encrypt-text-bctextencoder)

#### 1.7 Perform Multi-layer Hashing using CyberChef
CyberChef enables a wide array of "cyber" tasks directly in browser. It offers a wide range of operations and transformations, from basic text manipulation to complex cryptographic functions which include various hashing techniques such as MD5, SHA-1, SHA-256, SHA-512, etc., and encoding techniques such as text to hexadecimal, binary, Base64, or URL encoding.

A multi-layer hash typically refers to a hierarchical or nested structure of hash functions applied successively to data. Instead of just applying a single hash function to a piece of data, multiple hash functions are employed in layers or stages, with the output of one hash function serving as the input to the next one.

Create a new text file Secret.txt and open it. Write some text in it (here, My Account number is 0234569198) and press Ctrl+S to save the file. Close the text file.

Launch any web browser, and visit

[CyberChef](https://gchq.github.io/CyberChef/)

---

### 2. Create a self signed Certificate
In cryptography and computer security, a self-signed certificate is an identity certificate signed by the same entity whose identity it verifies.

#### 2.1 Create and use self signed certificates

**Steps**:    
1. Click the Type here to search icon present in the bottom-left of Desktop and type iis. Select Internet Information Services (IIS) Manager from the results
2. The Internet Information Services (IIS) Manager window appears; click the machine name (SERVER2019 (SERVER2019\Administrator)) under the Connections section from the left-hand pane.
3. In SERVER2019 Home, double-click Server Certificates in the IIS section.
4. The Server Certificates wizard appears; click Create Self-Signed Certificate… from the right-hand pane in the Actions section.
5. The Create Self-Signed Certificate window appears; type GoodShopping in the Specify a friendly name for the certificate field. Ensure that the Personal option is selected in the Select a certificate store for the new certificate field; then, click OK.
6. A newly created self-signed certificate will be displayed in the Server Certificates pane, as shown in the screenshot.
7. Expand the Sites node from the left-hand pane, and select GoodShopping from the available sites. Click Bindings… from the right-hand pane in the Actions section.
8. The Site Bindings window appears; click Add….
9. The Add Site Binding window appears; choose https from the Type field drop-down list. Once you choose the https type, the port number in the Port field automatically changes to 443 (the channel on which HTTPS runs).
10. Choose the IP address on which the site is hosted (here, 10.10.1.19).
11. Under the Host name field, type www.goodshopping.com. Under the SSL certificate field, select GoodShopping from the drop-down list, and click OK.
12. The newly created SSL certificate is added to the Site Bindings window; then, click Close.
13. Now, right-click the name of the site for which you have created the self-signed certificate (here, GoodShopping) and click Refresh from the context menu.
14. Minimize the Internet Information Services (IIS) Manager window.
15. Open the Mozilla Firefox browser and go to https://www.goodshopping.com.
16. The Warning:Potential Security Risk Ahead message appears, click Advanced… to proceed.
17. Click Accept the Risk and Continue.
18. Now you can see Goodshopping webpage with ssl certificate assigned to it, as shown in the screenshot.

---

### 3. Perform Disk Encryption
Disk encryption is a technology that protects the confidentiality of the data stored on a disk by converting it into an unreadable code using disk encryption software or hardware.

#### 3.1 Disk Encryption using Veracrypt
VeraCrypt is a software used for establishing and maintaining an on-the-fly-encrypted volume (data storage device). On-the-fly encryption means that data is automatically encrypted just before it is saved, and decrypted just after it is loaded, without any user intervention. No data stored on an encrypted volume can be read (decrypted) without using the correct password/keyfile(s) or correct encryption keys. The entire file system is encrypted (e.g., file names, folder names, free space, metadata, etc.).

**Steps**:
- Create a new encrypted volume

<img width="562" height="486" alt="image" src="https://github.com/user-attachments/assets/ddbe6b07-6c4e-4b14-b92f-dced8bfaa8d9" />

<img width="527" height="424" alt="image" src="https://github.com/user-attachments/assets/2299c10d-9bad-4c74-b5fb-ede22d1bc192" />

- Check the random box

<img width="679" height="432" alt="image" src="https://github.com/user-attachments/assets/16b3509a-decc-472d-88fb-0e786430fccc" />

- To use mount it

<img width="561" height="483" alt="image" src="https://github.com/user-attachments/assets/d1ec781c-6f84-448a-b41e-944c6d09af69" />


#### 3.2 Disk Encryption using Bitlocker
Turn BitLocker on for completer disk encryption

#### 3.3 Disk Encryption using Rohos
[Rohos Disk Encryption](https://rohos.com/products/rohos-disk-encryption/)

Create a new encrypted disk    
<img width="618" height="348" alt="image" src="https://github.com/user-attachments/assets/c6e26dc6-ee8d-47aa-a645-dfbc453e6613" />
<img width="394" height="358" alt="image" src="https://github.com/user-attachments/assets/120e2695-27de-4dee-ad13-87bd3e76b20c" />

