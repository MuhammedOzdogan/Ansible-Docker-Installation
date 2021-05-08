
# Ansible Docker Installation 

This Ansible repository makes ready to use docker in a linux machine. 

- Install [docker](https://docs.docker.com/engine/install/ubuntu/)

- Configure [post installation steps](https://docs.docker.com/engine/install/linux-postinstall/) to manage docker as a **non-root user**

- Install [docker-compose](https://docs.docker.com/compose/install/) .

    
# Edit Inventory File

    ---
    droplets:
      hosts:
        droplet1:
          ansible_host: droplet # Ip address or the hostname defined in /etc/hosts file
          ansible_user: sem
          ansible_ssh_private_key_file: ~/.ssh/sem-ecdsa
          ansible_sudo_pass: "{{my_cluster_sudo_pass}}"


 - **droplets** is just the group name. You can use this notation to group your hosts. You can put the hosts on DigitalOcean to droplets group or Google Cloud machines to
   gc etc. 
 - **droplet1** is the name of my remote host you can use the ip address of your remote machine or the name that you give  in /etc/hosts file.
   
 - **ansible_user** is the username that you want to login that machine via ssh.

Please edit these lines for your own infrastructure.


# Store sudo password in a vault file
Please run the command below, this command creates a [vault file](https://docs.ansible.com/ansible/latest/user_guide/vault.html#creating-encrypted-files) to store your password.

    ansible-vault create passwd.yml

Set the password for vault. After providing a password, the tool will start whatever editor you have defined with `$EDITOR`. Append the following

    my_cluster_sudo_pass: your_sudo_password_for_remote_servers

Finally close and save the file.

# Run
Open your terminal and run this command.

    ansible-playbook -i inventory.yml--ask-vault-pass --extra-vars '@passwd.yml' main.yaml

# How It Works
If you don't know how to use ansible you may want to visit [this](https://www.ansible.com/resources/get-started) page.

## Optional Step:

If you add the ip address of your remote machine into the `/etc/hosts`. You can access the remote machine via its name instead of ip address. Check the last line:
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
    1.2.3.4	          ec2
    123.123.123.123   droplet


# Support
This playbook just works on Ubuntu and Debian machines. You can make a pull request to support other distros. It's just about adding the other the package managers and docker gpg urls. 