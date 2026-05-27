# Tech Notes

## what is SSh :

SSH, or secure shell, is a secure protocol and the most common way of safely administering remote servers. Using a number of encryption technologies, SSH provides a mechanism for establishing a cryptographically secured connection between two parties, authenticating each side to the other, and passing commands and output back and forth.

### 1. Symmetric Encryption :

Symmetrical encryption is a type of encryption where one key can be used to encrypt messages to the opposite party, and also to decrypt the messages received from the other participant. There is typically only a single key that is used for all operations. _Symmetric keys_ are used by SSH in order to encrypt the entire connection. Contrary to what some users assume, public/private asymmetrical key pairs that can be created are only used for authentication, not encrypting the connection. The client and server both contribute toward establishing this key, and the resulting secret is never known to outside parties. The secret key is created through a process known as a _key exchange algorithm_. This exchange results in the server and client both arriving at the same key independently by sharing certain pieces of public data and manipulating them with certain secret data.The symmetrical encryption key created by this procedure is session-based and constitutes the actual encryption for the data sent between server and client.

### 2. Asymmetric Encryption :

_Asymmetrical encryption_ is different from symmetrical encryption because to send data in a single direction, two associated keys are needed. One of these keys is known as the private key, while the other is called the public key. The _public key_ can be freely shared with any party. The mathematical relationship between the public key and the private key allows the public key to encrypt messages that can only be decrypted by the private key. This is a one-way ability, meaning that the public key has no ability to decrypt the messages it writes. The _private key_ should be kept entirely secret and should never be shared with another party. The more well-discussed use of asymmetrical encryption with SSH comes from SSH key-based authentication. SSH key pairs can be used to authenticate a client to a server. The client creates a key pair and then uploads the public key to any remote server it wishes to access. This is placed in a file called authorized\_keys within the ~/.ssh directory in the user account's home directory on the remote server.

After the symmetrical encryption is established to secure communications between the server and client, the client must authenticate to be allowed access. The server can use the public key in this file to encrypt a challenge message to the client. If the client can prove that it was able to decrypt this message, it has demonstrated that it owns the associated private key.

### 3. How ssh works :

The SSH protocol employs a client-server model to authenticate two parties and encrypt the data between them.

The server component listens on a designated port for connections. It is responsible for negotiating the secure connection, authenticating the connecting party, and spawning the correct environment if the credentials are accepted.

The client is responsible for beginning the initial transmission control protocol (TCP) handshake with the server, negotiating the secure connection, verifying that the server's identity matches previously recorded information, and providing credentials to authenticate.

An SSH session is established in two separate stages. The first is to agree upon and establish encryption to protect future communication. The second stage is to authenticate the user and discover whether access to the server should be granted.

### 3.1. Negotiating Encryption for the session :

When a TCP connection is made by a client, the server responds with the protocol versions it supports. If the client can match one of the acceptable protocol versions, the connection continues. The server also provides its public host key, which the client can use to check whether this was the intended host.

At this point, both parties negotiate a session key using a version of something called the _Diffie-Hellman algorithm_. This algorithm (and its variants) make it possible for each party to combine their own private data with public data from the other system to arrive at an identical secret session key.

The session key will be used to encrypt the entire session. The public and private key pairs used for this part of the procedure are completely separate from the SSH keys used to authenticate a client to the server.

### 3.2. Authenticating the user access to the server :

The general method is password authentication, which is when the server prompts the client for the password of the account they are attempting to log in with. The password is sent through the negotiated encryption, so it is secure from outside parties.

Even though the password will be encrypted, this method is not generally recommended due to the limitations on the complexity of the password. Automated scripts can break passwords of normal lengths very easily compared to other authentication methods.

The most popular and recommended alternative is the use of SSH key pairs. SSH key pairs are asymmetric keys, meaning that the two associated keys serve different functions.

The public key is used to encrypt data that can only be decrypted with the private key. The public key can be freely shared, because, although it can encrypt for the private key, there is no method of deriving the private key from the public key.

Authentication using SSH key pairs begins after the symmetric encryption has been established as described in the previous section.

- The client begins by sending an ID for the key pair it would like to authenticate with to the server.
- The server checks the authorized\_keys file of the account that the client is attempting to log into for the key ID.
- If a public key with a matching ID is found in the file, the server generates a random number and uses the public key to encrypt the number.
- The client combines the decrypted number with the shared session key that is being used to encrypt the communication, and calculates the _MD5 hash_ of this value
- The server uses the same shared session key and the original number that it sent to the client to calculate the MD5 value on its own.

### 4. Why using ssh key pairs :

SSH keys are one of the most secure SSH authentication options. It is definitely more secure than the usual SSH password authentication. Therefore, it is highly recommended to use SSH Key authentication method for connections to your servers.

With password authentication, you can connect to your server from any location, you only need to fill in your password. However, if your password gets leaked, it is a major risk as anyone who knows your password will be able to get into the server.

SSH Key authentication only allows connections from clients whose key matches the one on the server.

### 5. Configure the config file
```
Host csnhr.nhr.fau.de csnhr

    HostName csnhr.nhr.fau.de

    User iwi1115h

    IdentityFile ~/.ssh/id_ed25519_fau

    IdentitiesOnly yes

    PasswordAuthentication no

    PreferredAuthentications publickey

    ForwardX11 no

    ForwardX11Trusted no
```
#### 5.1 Aliases for hostnames

Aliases are appended to the line starting with `Host`. For example, to use `csnhr` as an alias for `csnhr.nhr.fau.de` the original line `Host csnhr.nhr.fau.de` from the templates above is changed to `Host csnhr.nhr.fau.de csnhr`.
### 6. Creating ssh keys using Terminal  :

- Create the key pairs :

       ssh-keygen -t rsa
       ssh-keygen -t ed25519 -f <filename>
       ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519_nhr_fau
	     

- Upload your new SSH public key to your remote host by running the following command:

       ssh-copy-id username@remote-host-ip-address

- Log in to your remote host and edit your SSH config file:

       ssh username@remote-host-ip-address
       code .ssh config

- Scroll down the config file and make sure the following attributes are set correctly:

      RSAAuthentication yes
      PubkeyAuthentication yes
      PasswordAuthentication no


### ED25519

ED25519 is a public-key cryptographic algorithm used for digital signature generation and verification. It is based on the elliptic curve cryptography and is considered more secure than other commonly used algorithms, such as RSA and DSA.

An ED25519 key pair consists of a private key and a corresponding public key. The private key is used to generate digital signatures, while the public key is used to verify the signatures.

The ED25519 algorithm is based on the elliptic curve defined over the prime field of 2²⁵⁵-19. The private key is a 256-bit integer, while the public key is a 32-byte sequence.

Example: Let’s say Alice wants to send a message to Bob, and she wants to make sure that the message is not altered during transmission. Alice can use ED25519 to generate a digital signature for the message and send the signature along with the message to Bob. Bob can then use Alice’s public key to verify the signature and make sure that the message is authentic.

## What is X11 forwarding:

### 1. Overview

The secure shell (SSH) is a handy tool for running remote processes on a local Linux system. Inevitably, while using SSH, we encounter the need to display graphical interfaces from the remote system on our local screen. X11 port forwarding/tunneling facilitates this seamlessly and securely.

### 2. X Forwarding Configuration

For clarity, we'll use the terms server and client to reference the remote and _local_ Linux systems, respectively. The server must be able to perform X server authorization for X forwarding to work**. In addition, we must enable X forwarding on both the server and the client systems. Let's see how to perform each of these steps in detail.

### 2.1. X Server Authorization

The X server is a fundamental component of the X Window System, which provides the graphical foundation for Unix-based systems. On Linux, the X server is typically pre-installed, meaning it comes with the operating system. However, on Windows, which doesn't use the X Window System natively, additional software is needed to provide X server functionality.

**Windows uses a different graphical system, and it doesn't natively support the X Window System used by Linux**. **When you connect to a Linux machine and want to display graphical applications on your Windows machine, you need additional software to act as an X server.**

**Xming and VcXsrv are popular X server implementations for Windows**. They allow Windows machines to display graphical applications from remote Linux servers that use X11 forwarding.

In **VcXsrv settings** allow connection from any client and then when launching bonxai\_ros it will show you rviz2 window

We need to confirm that xauth is installed on the server for X forwarding to work. The x_auth utility handles authorization of the X server information on UNIX systems. Let's quickly check whether it is installed:

$ which xauth
/usr/bin/xauth
Copy

Luckily, _xauth_ comes installed in most standard Linux systems. In Section 3, we shall see how to install it if needed.

### 2.2. Enabling X Forwarding on Server

To enable X forwarding on the server-side, we simply add the following option to the ssh config file: 

X11Forwarding yes


### **2.3. Enabling X Forwarding on the Local System**

Once we have enabled X-forwarding on the server, we can now run the usual SSH command with an additional _-Y_ option:

     ssh -Y username@server

Now, we can simply interact with graphical interfaces in our local system, while their processes run on the remote server.

**In git bash :**

You need to set the display before ssh to the server and set it as the display that is used by your xserver program : 

     export DISPLAY=127.0.0.1:0.0
     ssh –Y jetsonaxorin

**In vscode :**

First you need to set the variable **DISPLAY** in **terminal integrated env linux** as :

     "terminal.integrated.env.linux": {

     "DISPLAY": "127.0.0.1:0.0"

     }

Then you do not need to set the display in vscode explicitly  anymore, it will be always set to this above so just run your program in vscode (rviz2)



## SSL

SSL, or Secure Sockets Layer, is an encryption for the purpose of ensuring privacy, authentication, and data integrity in Internet communications. SSL is the predecessor to the modern [TLS] encryption used today.

A website that implements SSL/TLS has [HTTPS] in its URL instead of [HTTP].

### How does SSL works?

- In order to provide a high degree of [privacy], SSL encrypts data that is transmitted across the web. This means that anyone who tries to intercept this data will only see a garbled mix of characters that is nearly impossible to decrypt.
- SSL initiates an  **authentication**  process called a [handshake] between two communicating devices to ensure that both devices are really who they claim to be.
- SSL also digitally signs data in order to provide  **data integrity** , verifying that the data is not tampered with before reaching its intended recipient.

### Why SSL is important?

- Originally, data on the Web was transmitted in plaintext that anyone could read if they intercepted the message. For example, if a consumer visited a shopping website, placed an order, and entered their credit card number on the website, that credit card number would travel across the Internet unconcealed.
- SSL was created to correct this problem and protect user privacy. By encrypting any data that goes between a user and a web server, SSL ensures that anyone who intercepts the data can only see a scrambled mess of characters. The consumer's credit card number is now safe, only visible to the shopping website where they entered it.
- SSL also stops certain kinds of cyber attacks: It authenticates web servers, which is important because attackers will often try to set up fake websites to trick users and steal data. It also prevents attackers from tampering with data in transit, like a tamper-proof seal on a medicine container.

### What is an SSL Certificate?

SSL can only be implemented by websites that have an [SSL certificate] (technically a "TLS certificate"). An SSL certificate is like an ID card or a badge that proves someone is who they say they are. SSL certificates are stored and displayed on the Web by a website's or application's server.

One of the most important pieces of information in an SSL certificate is the website's public [key] makes encryption and authentication possible. A user's device views the public key and uses it to establish secure encryption keys with the web server. Meanwhile the web server also has a private key that is kept secret; the private key decrypts data encrypted with the public key.

Certificate authorities (CA) are responsible for issuing SSL certificates.

## What is public key cryptography?

Public key cryptography is a method of encrypting or signing data with two different keys and making one of the keys, the public key, available for anyone to use. The other key is known as the private key. Data encrypted with the public key can only be decrypted with the private key. Because of this use of two keys instead of one, public key cryptography is also known as [asymmetric cryptography]. It is widely used, especially for [TLS/SSL], which makes [HTTPS]possible.

### What is a cryptographic key?

In cryptography, a [key] is a piece of information used for scrambling data so that it appears random; often it's a large number, or string of numbers and letters. When unencrypted data, also called plaintext, is put into a cryptographic algorithm using the key, the plaintext comes out the other side as random-looking data. However, anyone with the right key for decrypting the data can put it back into plaintext form.

For example, suppose we take a plaintext message, "hello," and encrypt it with a key; let's say the key is "2jd8932kd8." Encrypted with this key, our simple "hello" now reads "X5xJCSycg14=", which seems like random garbage data. However, by decrypting it with that same key, we get "hello" back.

### How does TLS/SSL use public key cryptography?

Public key cryptography is extremely useful for establishing secure communications over the Internet (via HTTPS). A website's [SSL/TLS certificate]  which is shared publicly, contains the public key, and the private key is installed on the [origin server] it's "owned" by the website.

[TLS handshakes] use public key cryptography to authenticate the identity of the origin server, and to exchange data that is used for generating the session keys. A key exchange algorithm, such as RSA or Diffie-Hellman, uses the public-private key pair to agree upon session keys, which are used for symmetric encryption once the handshake is complete. Clients and servers are able to agree upon new session keys for each communication session, so that bad actors are unable to decrypt communications even if they identify or steal one of the session keys from a previous session.

## What is HTTPS?

Hypertext transfer protocol secure (HTTPS) is the secure version of [HTTP], which is the primary protocol used to send data between a web browser and a website. HTTPS is encrypted in order to increase security of data transfer. This is particularly important when users transmit sensitive data, such as by logging into a bank account, email service, or health insurance provider.

Any website, especially those that require login credentials, should use HTTPS. In modern web browsers such as Chrome, websites that do not use HTTPS are marked differently than those that are. Look for a padlock in the URL bar to signify the webpage is secure. Web browsers take HTTPS seriously; Google Chrome and other browsers flag all non-HTTPS websites as not secure.