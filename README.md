# PasswordManager
# Passbolt Password Manager Hosted in Cloud

Project Overview:

This project involves hosting a password manager in the cloud to develop and demonstrate skills in secure access management and cloud-based security solutions. It focuses on safeguarding sensitive data and fortifying systems against potential threats, showcasing expertise in implementing robust security measures for cloud environments.

Project Details:

I set up:

- **Cloud-Based Virtual Machine**: Deployed a virtual machine in the cloud to host the password manager application, ensuring a secure and scalable environment.
- **Password Manager Application**: Installed and configured a password manager software, implementing secure access controls and encryption to protect sensitive data.

## Passbolt

- **Open Source**: Free to use and can be self-hosted.
- **User Management**: Allows role-based access control to manage who can see and edit passwords.
- **End-to-End Encryption**: Ensures that passwords are encrypted on the client-side before being sent to the server.
- **Integration**: Supports integration with various tools and services via plugins and APIs.
- **Browser Extension**: Available for major browsers to autofill passwords and manage credentials easily.
- **Team Collaboration**: Designed for teams to share passwords securely and collaborate on access management.

## 1. Deploying Cloud Based Passbolt Instance

- Starting by navigating to the official Passbolt website to explore available deployment options for different environments.
- Choosing the AWS deployment option to leverage Amazon Web Services for hosting Passbolt securely and reliably.
- Passbolt offers an Amazon Machine Image (AMI) on the AWS Marketplace. This pre-configured server image simplifies the deployment process, ensuring you have all necessary components ready to go.
![Passbolt_Download](https://github.com/0xFroggi/PasswordManager/blob/main/images/passbolt_aws_download.png?raw=true)

## 2. Launching Passbolt Instance

- Selecting the Passbolt AMI and click "Continue to Subscribe" to add it to your account.
- Proceed to "Continue to Configuration" and select your preferred region to ensure optimal performance and compliance with data residency requirements.
- Choosing an appropriate instance type based on your performance needs (e.g., t2.micro for small setups, larger instances for more demanding environments).
- t2.meduim is the recommended instance type by Passbolt. It is not qualified for free tier but cheaper options are available as well.
![Passbolt_Pricing](https://github.com/0xFroggi/PasswordManager/blob/main/images/passbolt_pricing.png?raw=true)

- Configuring instance details, including Virtual Private Cloud (VPC) settings, subnet, and the option to auto-assign a public IP address for easy access.
- Setting up security groups to control inbound and outbound traffic. Open ports 80 (HTTP) and 443 (HTTPS) for web access, and port 22 (SSH) for secure remote access to the instance (as they are recommended by Passbolt).
![Passbolt_Security_Groups](https://github.com/0xFroggi/PasswordManager/blob/main/images/passbolt_security_settings.png?raw=true)

- It is good practice to limit the IP addresses which can access to the instance through these ports.
- Selecting an existing key pair or create a new one to facilitate secure SSH access to the instance. This key pair is crucial for maintaining the security of your administrative access.
![Passbolt_keypair](https://github.com/0xFroggi/PasswordManager/blob/main/images/passbolt_keypair.png?raw=true)

- Key pairs can be generated through terminal in the Linux machines.
- Example command:

```
ssh-keygen -t rsa -b 2048 -C "your_email@example.com"
```

- Follow the prompts to save the key pair to your desired location, typically `~/.ssh/id_rsa` for the private key and `~/.ssh/id_rsa.pub` for the public key.
![Passbolt_keypair2](https://github.com/0xFroggi/PasswordManager/blob/main/images/passbolt_importKeypair.png?raw=true)

- Launching the instance and waiting for it to be provisioned. Note the public IP address assigned to the instance, which will be used to access the Passbolt application.
![Passbolt_launched](https://github.com/0xFroggi/PasswordManager/blob/main/images/passbolt_EC2Dash.png?raw=true)

## 3. Accessing the Passbolt and Discovering the Password Generation

- Opening a web browser and navigating to the public IP address of the instance to access the Passbolt web interface and begin the setup process.
![Passbolt_config](https://github.com/0xFroggi/PasswordManager/blob/main/images/passbolt_dash.png?raw=true)

- It is important to configure SSL access to the Passbolt web application. There are few ways to do it, here is an example process for configuring SSL:
    - Use Certbot to obtain an SSL certificate for your domain from Let’s Encrypt.
    - Configure Nginx to use the SSL certificate and redirect HTTP traffic to HTTPS.
    - Ensure automatic renewal of SSL certificates with Certbot and update Passbolt's configuration for the correct domain and SSL settings.
- Finally Passbolt is ready to use.
![Passbolt_dash](https://github.com/0xFroggi/PasswordManager/blob/main/images/passbolt_installed.png?raw=true)

- Here is randonly generated password and its entropy value:
![Passbolt_passgen](https://github.com/0xFroggi/PasswordManager/blob/main/images/passbolt_pasgen.png?raw=true)

# Importance of Entropy and Randomness

- **Entropy**:
    - Measures the randomness or unpredictability in a password.
    - Higher entropy indicates a more complex and secure password.
    - Calculated in bits; each additional bit doubles the possible combinations.
- **Randomness**:
    - Essential for creating secure passwords that are difficult to predict.
    - Involves using a variety of characters (uppercase, lowercase, numbers, special symbols).
    - Reduces the likelihood of successful brute force or dictionary attacks.
- **Importance**:
    - High entropy and randomness in passwords protect against guessing and cracking attempts.
    - Enhances overall security by making it harder for attackers to compromise accounts.
    - Critical for safeguarding sensitive data and maintaining robust security practices.
    

# Cryptographic techniques used by Passbolt

- **OpenPGP Encryption**:
    - Passbolt utilizes OpenPGP, an encryption standard that provides cryptographic privacy and authentication.
    - Each user has a pair of OpenPGP keys (public and private keys). The public key is used to encrypt data, while the private key is used to decrypt it.
- **End-to-End Encryption**:
    - Passwords and sensitive data are encrypted on the client side before being sent to the server. This ensures that only the intended recipients (who possess the correct private keys) can decrypt and access the data.
    - This encryption is done using the recipient's public key, making sure that only the corresponding private key can decrypt the data.
- **Key Management**:
    - Users generate their own OpenPGP key pairs during account creation.
    - Passbolt manages the distribution and verification of public keys to ensure secure communication.
- **Server Security**:
    - The server stores encrypted data and does not have access to the private keys needed to decrypt the data.
    - This means that even if the server is compromised, the attacker cannot decrypt the stored passwords without the user's private keys.
    
    # Summary
    
    In this project, I deployed Passbolt, an open-source password manager, in a cloud environment. The setup involved configuring a secure cloud-based virtual machine, implementing SSL for secure web access, and ensuring high entropy in generated passwords to enhance security. This project showcases skills in secure access management, cloud-based security solutions, and the ability to safeguard sensitive data against potential threats.

