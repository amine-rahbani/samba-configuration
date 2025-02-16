# Samba Installation and Configuration on Linux  

## 📌 Description  
This project provides a step-by-step guide to installing and configuring **Samba** on a Linux (Fedora Workstation) server to facilitate file and printer sharing with Windows and Linux clients using the **SMB (Server Message Block)** protocol.  

## 📹 Live Demonstration  
🎥 **[Watch the Samba Demo](https://drive.google.com/file/d/115SW7ip4nXJHmMK2KIqX0naoLMceYqgF/view?usp=sharing)** 


## 📁 Contents  
The guide covers the following topics:  
- 📌 Introduction to **Samba** and how it works  
- 🖥️ Installation and configuration of the Samba server  
- 💻 Configuration of Windows and Linux clients  
- 🔒 Accessing shared files with login and password  
- 🔓 Anonymous access to shared files  
- 🛠️ Troubleshooting and validation  

## 🚀 Installation and Configuration  

### 📌 1. Install Samba on the Server  
Run the following command to install Samba on Fedora:  
```sh  
dnf install samba -y  
```  
Verify the installation and check the installed version:  
```sh  
smbd --version  
```  

### 📌 2. Create a Shared Folder  
Create a folder for file sharing:  
```sh  
mkdir -p /home/samba/SharedFolder  
```  
Set appropriate permissions:  
```sh  
chown -R nobody:nogroup /home/samba/SharedFolder  
chmod -R 777 /home/samba/SharedFolder  
```  

### 📌 3. Configure the Samba Server  
Modify the Samba configuration file `/etc/samba/smb.conf` and add:  
```ini  
[SharedFolder]  
   path = /home/samba/SharedFolder  
   browsable = yes  
   writable = yes  
   guest ok = yes  
   read only = no  
```  
Restart the Samba service:  
```sh  
systemctl restart smb nmb  
systemctl enable smb nmb  
```  

### 📌 4. Access Samba Shared Folder  

#### 🔹 **From Windows (Graphical Mode)**  
1. Open **File Explorer**  
2. Enter `\\[SERVER_IP]` in the address bar  
3. Log in using the Samba credentials  

#### 🔹 **From Linux (Command Line Mode)**  
List available shares:  
```sh  
smbclient -L //[SERVER_IP] -U [username]  
```  
Access the shared folder:  
```sh  
smbclient //[SERVER_IP]/SharedFolder -U [username]  
```  

## 🛠️ Troubleshooting  
- Check if Samba is running:  
  ```sh  
  systemctl status smb nmb  
  ```  
- Test the configuration:  
  ```sh  
  testparm  
  ```  
- Verify the server's IP address:  
  ```sh  
  ip a  
  ```  

## 🐝 Author  
**Amine Rahbani** - _University Project 2024/2025_  


