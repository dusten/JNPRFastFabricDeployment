Standard Install. Install OpenSSH server. Everything else can be default. 

We are using ansible. Ansible uses python. We need to install python. 

~sudo apt-get install python-pip python-dev libxml2-dev libxslt-dev libssl-dev libffi-dev -y~

Pip is temperamental. If you don’t upgrade it and need help from the community they will tell you to upgrade first. Do the double upgrade just to cover your bases.
~sudo -H pip install --upgrade pip~

Here are the Juniper libraries we need to make the 
~sudo -H pip2 install junos-eznc
~sudo -H pip2 install jxmlease

We want the 2.4 version of Ansible. Mostly because if you have to fix it there is a lot more logging and it has more granularity in error messages.

Add the following line to /etc/apt/sources.list:
deb http://ppa.launchpad.net/ansible/ansible/ubuntu xenial main

then enter the following 
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367

sudo apt-get update

sudo apt-get install ansible -y


Now we need to install our ansible module.
Good news Ansible’s updates servers are on the most current module. Bad news, all of the automation I wrote is on the old version. Good news, the old stuff still works on the new stuff. I am working to upgrade to the new ansible verbiage and model.

ansible-galaxy install Juniper.junos,1.4.3   <— Case sensitive

sudo vi etc/hosts file with all of your clients in it. This will make ansible inventory file work faster and easier.

jnpradmin@AutoMach:~/BaseConfig/03-IP-Address$ more /etc/hosts
127.0.0.1	localhost
127.0.1.1	AutoMach
192.2.0.9	QFX5110-32Q-9
192.2.0.10	QFX5110-32Q-10


# The following lines are desirable for IPv6 capable hosts
::1     localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters

Enter the command:
ssh-keygen 

ssh to all of your hosts for the last time and input the key or use the python script in this directory. 

set system login user jnpradmin uid 2005 class super-user authentication ssh-rsa "ssh-rsa ThisIsTheKeyYouJustMadeBecauseYouAreAwesome jnpradmin@AutoMach"

commit and quit. 

Login to each networking device from the virtual machine and accept the key from the machine. You’ll note there’s no password entry now the the key is complete.

git clone https://github.com/packetjanitor/JNPRFastFabricDeployment.git

I will cover the ansible configuration tools in their repspective directories a little later. 