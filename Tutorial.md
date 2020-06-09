*******************************
# ***Setting up Virtual Machine (VM)***
*******************************

Setting up process of VM is pretty straightforward. 
The user should give:
    - 8GB of RAM to the machine (or less, rule of thumb is 50% of RAM from the host machine) 
    - ⋅⋅10GB of Memory
    
    
    
*******************************
#***Installation Process***
******************************    

Installation process is also pretty straightforward. User just needs to select basic settings (language, keyboard-layour)
and his username, server's name and a password.
All other settings can be left as they were, with just one excpetion:
    -In installation menu "SSH Setup" user should select to install "OpenSSH".
    
    
    
    
    
*******************************
# ***Configuration of files***
******************************    



Next parts consits of modifying and creating files needed in order for server to be accessible from host machine.

Steps that need to be done are:
  
  ***Modifying sshd_Config file***
  ------------------------------------------------------------
  - User needs to open sshd_config file in order to modify it, using the nano text editor
  - command is: sudo nano/etc/ssh/sshd_config 
  ------------------------------------------------------------
  
  
  ***Changing port***
  ------------------------------------------------------------
  - User needs to delete "#" symbol infront of the "port 22" and change value to 1900
  ------------------------------------------------------------
  
  
  
  ***Deactivating permitrootlogin***
  ------------------------------------------------------------
  - User needs to change the value of permitrootlogin to "no"
  - This will deactivate permitrootlogin, so that only users that are not root can sign it
  ------------------------------------------------------------
  
  
  ***Modifying Port Forwarding in VM***
  ------------------------------------------------------------
  - User needs to modify port forwarding settings in VM, in order to connect to the Ubuntu Server inside VM.
  - Value for Host IP: 127.0.0.1
  - Value for Host Port: 2020
  - Value for Guest IP: 10.0.2.15
  - Value for Guest Port: 1900
  ------------------------------------------------------------
  
  
  ***Log in via CMD and test the connection***
  ------------------------------------------------------------
  - User needs to log to Ubuntu Server inside VM via CMD
  - In cmd the user needs to type this command with his username (in my case that is lazargrbovic)
  - Ssh -p 1900 lazargrbovic@127.0.0.1
  ------------------------------------------------------------
  
  
  ***Generating rsa key for the ssh***
  ------------------------------------------------------------
  - In cmd user needs to type in: ssh-keygen -t rsa
  ------------------------------------------------------------
  
  ***Getting into VM***
  ------------------------------------------------------------
  - In CMD: scp -P 2020 C:\Users\Lazar\.ssh\id_rsa.pub lazargrbovic@127.0.0.1:/home/lazargrbovic
  - Scp is used to copy data, and with this command I will copy ssh key to the Virtual Machine
  - User's ssh on his computer is "id_rsa.pub"
  - Now instead of using his password, user can give his ssh key when logging in
  ------------------------------------------------------------
  
  ***Commands inside VM (in the Ubuntu Server)***
  ------------------------------------------------------------
  - mkdir .ssh (**In this directory the settings for ssh will be saved**)
  - touch .ssh/authorized_keys (**Create authorized keys**)
  - cat id_rsa.pub >> .ssh/authorized_keys (**Copies the keys**)
  - sudo nano /etc/ssh/sshd_config (**Modifying again the config file using nano text editor, in order to remove comment by      pubkeyauthentication to "yes"**)
  ------------------------------------------------------------
  
  ***Connecting to server***
  ------------------------------------------------------------
  - ssh -p 2020 lazargrbovic@127.0.0.1 
  - With the command above, user can connect to server, and now he won't need to enter password anymore
  ------------------------------------------------------------
  
  
  ***Modifying again the ssh_config***
  ------------------------------------------------------------
  - sudo nano /etc/ssh/sshd_config
  - With this file user can edit "sshd_config" file inside a nano text editor, and user should set "PasswordAuthentication" to no
  - This will turn of the password authentication
  ------------------------------------------------------------
  
  ***Opening the port 1900 in firewall for ssh***
  ------------------------------------------------------------
  - sudo ufw allow 1900
  ------------------------------------------------------------
  
  ***Closing all other ports for incoming connections***
  ------------------------------------------------------------
  - sudo ufw default deny
  ------------------------------------------------------------
  
  
  ***Activating the firewall***
  ------------------------------------------------------------
  - sudo ufw enable
  ------------------------------------------------------------
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
