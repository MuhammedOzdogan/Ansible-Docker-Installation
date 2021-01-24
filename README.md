
# Ansible Docker Installation 

With this playbook you can install **docker**, configure post installation steps to manage docker as a **non-root user** and  install **docker-compose** .



## Optional Step:

Before you start you may want to configure hosts file for simplicity.
If you add your ip address of your remote machine to here and give a name to it. You can access it via its name instead of ip address. Check the last line:
**ec2** is the name of my remote server. Instead of `$ ping 1.2.3.4` I can do this `$ ping ec2`


**/etc/hosts**:

    127.0.0.1	localhost
    127.0.1.1	my-machine
    
    \# The following lines are desirable for IPv6 capable hosts
    ::1     ip6-localhost ip6-loopback
    fe00::0 ip6-localnet
    ff00::0 ip6-mcastprefix
    ff02::1 ip6-allnodes
    ff02::2 ip6-allrouters
    
    # **** Remote Servers ****
    1.2.3.4	ec2
    
# Edit Inventory File

    [aws]
    ec2 ansible_user=ubuntu

 - **aws** is just the group name. You can use this notation to group your hosts. You can put the hosts on Amazon to aws group or Google Cloud machines to
   gc etc. If you don't like this line you can delete it.
 - **ec2** is the name of my remote host you can use the ip address of your remote machine or the name that you give  in /etc/hosts file.
   
 - **ansible_user** is the username that you want to login that machine.

Edit these lines and you are ready to go.

# Run
Open your terminal and run this command.

    ansible-playbook -i hosts main.yaml

# How It Works
If you don't know how to use ansible you may want to visit [this](https://www.ansible.com/resources/get-started) page.

# Support
This playbook just works on Ubuntu and Debian machines. You can make a pull request to support other distros. It's just about adding the other the package managers and docker gpg urls. 