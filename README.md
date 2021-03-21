# AWS
Exploring AWS cloud platform
AWS Management Console,

AWS C

                                                           **7. Amazon EC2 - Launch Linux VM**

In this section i am going to explain how to create AMI (Amazon machine Image) instance where we can launch different flavours of OS(Operating systems)         like linux, windows and Mac. In this example i am creating an instance of Amazon linux AMI.

     1. Choose AMI : 
     
![choose AMI_1_AWS](https://user-images.githubusercontent.com/20144507/111040332-d0213300-8432-11eb-9143-a1e563141614.png)


     2. Choose Instance Type

![choose instance type_2_AWS](https://user-images.githubusercontent.com/20144507/111040371-ff37a480-8432-11eb-9540-84dfdb76da7d.png)

     
     
     3. Configure Instance
![configure instance_3 AWS](https://user-images.githubusercontent.com/20144507/111040411-21c9bd80-8433-11eb-9baa-fe79073bcb6d.png)
   
    4.Add Storage

![Add storage_4 AWS](https://user-images.githubusercontent.com/20144507/111040453-4756c700-8433-11eb-8e73-9046d172f890.png)

     
    5. Add Tags
![Add tags_5 AWS](https://user-images.githubusercontent.com/20144507/111040463-56d61000-8433-11eb-9f52-9bd78d1a8d07.png)

    
    
    6. Configure Security Group
 ![configure security group_6 AWS](https://user-images.githubusercontent.com/20144507/111040480-681f1c80-8433-11eb-9687-c6ff875503fb.png)

      
    7. Review
   
  ![create key pair linux ami instance](https://user-images.githubusercontent.com/20144507/111040967-28a5ff80-8436-11eb-9790-b15be9a78db1.png)

![launch status EC2 instance AWS](https://user-images.githubusercontent.com/20144507/111040505-7a00bf80-8433-11eb-9ce7-6098db9864b8.png)
Launched view1
![launched instance linux AMI_view1](https://user-images.githubusercontent.com/20144507/111040673-6efa5f00-8434-11eb-851d-72aae1991116.png)
launched view2
![launched instance linux AMI_view2 ](https://user-images.githubusercontent.com/20144507/111040674-715cb900-8434-11eb-9ac4-cb51a88e1ac6.png)
![Terminate instance linux AMI](https://user-images.githubusercontent.com/20144507/111040981-3fe4ed00-8436-11eb-88ef-6fda2157fcb7.png)
![Terminate instance linux AMI VIEW](https://user-images.githubusercontent.com/20144507/111040986-45dace00-8436-11eb-92de-4bbe96aea592.png)

Note : 

Amazon EC2 instances
 Amazon Elastic Block Store (EBS)
 
 Remotely run commands on an EC2 instance :
        
    Step 1. Create an Identity and Access Management (IAM) role
    Step 2. Create an EC2 instance
    Step 3. Update the Systems Manager Agent
    Step 4. Run a Remote Shell Script
    Step 5. Terminate Your Resources


**10. Amazon EC2 - Launch Wordpress website**
      
      Here i am launching a centOS wordpress image in linux ubuntu, Steps to follow 
      1. Create a new user as "centos" when you tried to run using root user it will ask you somethint like this.
      ssh -i "vasam.pem" root@ec2-54-216-61-140.eu-west-1.compute.amazonaws.com
      Please login as the user "centos" rather than the user "root".
      Follow following steps to create new user in linux ubuntu
      Step 1:  Add The User
      adduser vas
      Step 2: Grant Root Privileges
      usermod -aG sudo vas
      
      Step 3: Verify New User
      su - vas
      grep '^sudo' /etc/group
      sudo:x:27:vas
      
      if there is problem in the file you will see this error "vas is not in the sudoers file.  This incident will be reported."
      So we have to give root privilages to the user.
      
      How to Fix “Username is not in the sudoers file. This incident will be reported” in Ubuntu ?
      Do run the below commands to resolve this problems. unless if you can't give root privilages to the future new users you can not give privilages
      to the user so that it is not possible to access the SSH clients.
      which leads you can not access EC2 instances what you will create in the future. This step is very important. 
      For every EC2 instance you have to connect with different user and with root privilages. To connect to EC2 instant using SSH client.
      
    Finally i did create a New user called centos
    sravan@sravan-Aspire-E1-470P:~$ adduser centos
    adduser: Only root may add a user or group to the system.
    sravan@sravan-Aspire-E1-470P:~$ sudo bash
    sudo: unable to stat /etc/sudoers.d/README: Permission denied
    root@sravan-Aspire-E1-470P:~# pwd
    /home/sravan
    root@sravan-Aspire-E1-470P:~# chmod -R 777 /etc/sudoers.d
    root@sravan-Aspire-E1-470P:~# sudo bash
    sudo: /etc/sudoers.d is world writable
    root@sravan-Aspire-E1-470P:~# adduser centos
    Adding user `centos' ...
    Adding new group `centos' (1006) ...
    Adding new user `centos' (1008) with group `centos' ...
    Creating home directory `/home/centos' ...
    Copying files from `/etc/skel' ...
    Enter new UNIX password: 
    Retype new UNIX password: 
    passwd: password updated successfully
    Changing the user information for centos
    Enter the new value, or press ENTER for the default
	Full Name []: 
	Room Number []: 
	Work Phone []: 
	Home Phone []: 
	Other []: 
    Is the information correct? [Y/n] Y
    root@sravan-Aspire-E1-470P:~#  usermod -aG sudo centos
    root@sravan-Aspire-E1-470P:~# su -centos
    bash: entos: command not found
    root@sravan-Aspire-E1-470P:~# su - centos
    To run a command as administrator (user "root"), use "sudo <command>".
    See "man sudo_root" for details.

    centos@sravan-Aspire-E1-470P:~$ man sudo_root
    centos@sravan-Aspire-E1-470P:~$ grep '^sudo' /etc/group
    sudo:x:27:sravan,usr,centos
    
    centos@sravan-Aspire-E1-470P:~$ sudo cp -r /home/sravan/Documents/aws/vasam.pem /home/centos/
    sudo: /etc/sudoers.d is world writable
    
    centos@sravan-Aspire-E1-470P:~$ ssh -i "vasam.pem" root@ec2-54-216-61-140.eu-west-1.compute.amazonaws.com
    Load key "vasam.pem": Permission denied
    Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
    
    centos@sravan-Aspire-E1-470P:~$ sudo ssh -i "vasam.pem" root@ec2-54-216-61-140.eu-west-1.compute.amazonaws.com
    sudo: /etc/sudoers.d is world writable
    Please login as the user "centos" rather than the user "root".

    Connection to ec2-54-216-61-140.eu-west-1.compute.amazonaws.com closed.
    
    centos@sravan-Aspire-E1-470P:~$ sudo apt -get update
    sudo: /etc/sudoers.d is world writable
    E: Command line option 'g' [from -get] is not understood in combination with the other options.
    
    centos@sravan-Aspire-E1-470P:~$ sudo apt-get update
    sudo: /etc/sudoers.d is world writable
    Ign:1 cdrom://Ubuntu 16.04.3 LTS _Xenial Xerus_ - Release amd64 (20170801) xenial InRelease
    Ign:2 cdrom://Ubuntu 16.04.3 LTS _Xenial Xerus_ - Release amd64 (20170801) xenial Release
    Ign:3 cdrom://Ubuntu 16.04.3 LTS _Xenial Xerus_ - Release amd64 (20170801) xenial/main amd64 Packages
    
    centos@sravan-Aspire-E1-470P:~$ sudo apt-get upgrade
    sudo: /etc/sudoers.d is world writable
    Reading package lists... Done
    Building dependency tree       
    Reading state information... Done
    Calculating upgrade... Done
    The following packages were automatically installed and are no longer required:
    adobe-flash-properties-gtk cdbs dh-translations gcc-5-base:i386 gnat-4.9-base intltool kde-telepathy-desktop-applets
    kde-telepathy-filetransfer-handler kde-telepathy-send-file libasyncns0:i386 libflac8:i386 libgnat-4.9 libjpeg62 libogg0:i386 libossp-uuid16
    libpulse0:i386 libreadline5 libsamplerate0:i386 libsndfile1:i386 libspeexdsp1:i386 libstdc++6:i386 libvorbis0a:i386 libvorbisenc2:i386
    
    centos@sravan-Aspire-E1-470P:~$ sudo yum install -y https://s3.region.amazonaws.com/amazon-ssm-region/latest/linux_amd64/amazon-ssm-agent.rpm
    sudo: /etc/sudoers.d is world writable
    There are no enabled repos.
    Run "yum repolist all" to see the repos you have.
    You can enable repos with yum-config-manager --enable <repo>
    
    centos@sravan-Aspire-E1-470P:~$ yum-config-manager --enable
    You must be root to change the yum configuration.
    
    centos@sravan-Aspire-E1-470P:~$ sudo bash
    sudo: /etc/sudoers.d is world writable
    
    root@sravan-Aspire-E1-470P:~# yum-config-manager --enable

    

Step 3: Verify New User
      select wordpress EC2 AMI market place and connect to the instance from linux.
